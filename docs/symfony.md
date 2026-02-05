# Symfony

## Structure

- `bin/` : The famous bin/console file lives here (and other, less important executable files).
- `config/` : Contains configuration. You will configure routes, services and packages.
- `public/` : This is the document root for your project: you put any publicly accessible files here.
- `templates/` : All your Twig templates live here.
- `src/` : All your PHP code lives here.
- `var/` : This is where automatically-created files are stored, like cache files (var/cache/) and logs (var/log/).
- `vendor/` : Third-party (i.e. "vendor") libraries live here! These are downloaded via the Composer package manager.

## Evenements

Le contrôleur vérifie et nettoie les entrées de la route, puis va émettre un évènement avec la méthode `dispatch` qui prend en argument la constante du nom de l'évènement. 

```php
$eventDispatcher->dispatch($customerCreateEvent, TheliaEvents::CUSTOMER_CREATEACCOUNT);
```

L'objet évènement doit être créé avant avec les différentes informations :

```php
$customerCreateEvent = new ApyCustomerCreateOrUpdateEvent(
  $data['title'] ?? null,
  $data['firstname'] ?? null,
  $data['lastname'] ?? null
);
```

Une (ou plusieurs) action(s) écoutent les évènements et va exécuter à la suite des fonctions selon leur priorité (jusqu'à 256) :

```php
$arr[TheliaEvents::CUSTOMER_CREATEACCOUNT] = [
    ['create', 127],
    ['createCustomerFluxCRM', 127],
    ['beforeCreate', 129],
    ['afterCreate', 127],
    ['updateMainPhone', 126],
    ['createHybridAuthData', 126],
    ['handleIsRetailer', 126]
];
```

La fonction va recevoir en paramètre l'évènement source et son nom, et peut exécuter des actions de persistance :

```php
public function create(CustomerCreateOrUpdateEvent $event, $eventName, EventDispatcherInterface $dispatcher): void
{
    $customer = new CustomerModel();
    $this->createOrUpdateCustomer($customer, $event, $dispatcher);
}
```

## Commandes utiles

- `php bin/console debug:router` : Liste toutes les routes
- `php bin/console lint:twig` : Vérifie les templates Twig
- `php bin/console debug:twig` : Liste les informations de Twig
- `php bin/console make:controller <nom>` : Crée un nouveau contrôleur
