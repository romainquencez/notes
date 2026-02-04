# Thelia

## Commandes

https://doc.thelia.net/docs/commands

Lister les commandes existantes (dans le conteneur PHP) :

```
php Thelia
```

## Loops

https://doc.thelia.net/docs/loops

Permet de lister et filtrer une collection d'instances de modèles dans un template.

```html
<table>
  {loop name='apy_customers' type='apy_customers'}
    <tr>
      <td>{$firstname}</td>
    </tr>  
  {/loop}
</table>
```

On peut ajouter une condition en amont pour ne pas afficher un tableau vide si il n'y a pas de résultats par exemple :

```html
{ifloop rel="apy_customers"}
  ...boucle...
{/ifloop}
```

### Implémentation

Coté backend il faut créer un fichier dédié dans le dossier `Loop`, par exemple `ApyCustomerLoop`.

Créer une classe `ApyCustomerLoop` qui hérite de la classe Thelia `BaseI18nLoop` et de `PropelSearchLoopInterface` pour créer une loop Propel.

Elle doit implémenter obligatoirement 3 fonctions :

- `getArgDefinitions` : décrit les arguments (requis ou optionels, et types) de la loop.
- `buildModelCriteria` : crée la requête Propel avec les différents filtres, jointures etc... qui va retourner la collection d'objets.
- `parseResults` : crée les variables disponibles dans le template depuis les résultats de la requête.

### Exemple

``` php
class ApyCustomerLoop extends BaseI18nLoop implements PropelSearchLoopInterface {
    protected function getArgDefinitions(): ArgumentCollection
    {
        return new ArgumentCollection();
    }

    public function buildModelCriteria(): ModelCriteria
    {
        // liste des apyCustomers
        $apyCustomers = ApyCustomerQuery::create();

        // jointure sur la table customer
        $customerJoin = new Join(
            ApyCustomerTableMap::COL_CUSTOMER_ID,
            CustomerTableMap::ID,
            Criteria::INNER_JOIN
        );
        $apyCustomers
            ->addJoinObject($customerJoin, 'customer_join')
            ->withColumn(CustomerTableMap::FIRSTNAME, 'firstname')
            ->withColumn(CustomerTableMap::LASTNAME, 'lastname')
            ->withColumn(CustomerTableMap::EMAIL, 'email')
            ->withColumn(CustomerTableMap::CREATED_AT, 'created_at');

        // jointure optionnelle sur la table lang
        $langJoin = new Join(
            CustomerTableMap::LANG_ID,
            LangTableMap::ID,
            Criteria::LEFT_JOIN
        );
        $apyCustomers
            ->addJoinObject($langJoin, 'lang_join')
            ->withColumn(LangTableMap::TITLE, 'lang_title');

        // tri par apy_customer.id
        $apyCustomers->orderById();
        return $apyCustomers;
    }

    public function parseResults(LoopResult $loopResult)
    {
        /** @var ApyCustomer $apyCustomer */
        foreach ($loopResult->getResultDataCollection() as $apyCustomer) {
            $loopResultRow = new LoopResultRow($apyCustomer);
            $loopResultRow->set('id', $apyCustomer->getId());
            $loopResultRow->set('customerId', $apyCustomer->getCustomerId());
            $loopResultRow->set('firstName', $apyCustomer->getVirtualColumn('firstname'));
            $loopResultRow->set('lastName', $apyCustomer->getVirtualColumn('lastname'));
            $loopResultRow->set('email', $apyCustomer->getVirtualColumn('email'));
            $loopResultRow->set('createdAt', $apyCustomer->getVirtualColumn('created_at'));
            $loopResultRow->set('langTitle', $apyCustomer->getVirtualColumn('lang_title'));
            $loopResult->addRow($loopResultRow);
        }

        return $loopResult;
    }
}
```
