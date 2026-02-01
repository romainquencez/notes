# PHP

## Syntaxe

PHP inclut également la balise courte echo <?=, qui est un raccourci pour <?php echo.

```php
Vous pouvez utiliser la balise courte pour <?= 'écrire ce texte' ?>.
Est équivalent à <?php echo 'écrire ce texte' ?>.
```

Pour assigner par référence, ajoutez simplement un & (ET commercial) au début de la variable qui est assignée (la variable source).

```php
$foo = 'Pierre';              // Assigne la valeur 'Pierre' à $foo
$bar = &$foo;                 // Référence $foo avec $bar.
```

### Opérateur de contrôle d'erreur

PHP supporte un opérateur de contrôle d'erreur : l'arobase (@). Lorsque cet opérateur est ajouté en préfixe d'une expression PHP, les diagnostics d'erreurs qui peuvent être générés par cette expression seront ignorés.

```php
$value = @$cache[$key];
// la ligne ci-dessus n'affichera pas d'alerte si la clé $key du tableau n'existe pas
```

### Opérateurs fonctionnels

L'opérateur `|>`, ou « pipe », accepte une fonction callable à un seul paramètre à droite et lui transmet la valeur de gauche, le résultat étant la valeur renvoyée par la fonction callable.

```php
$result = "PHP Rocks"
    |> htmlentities(...)
    |> str_split(...)
    |> (fn($x) => array_map(strtoupper(...), $x))
    |> (fn($x) => array_filter($x, fn($v) => $v != 'O'))
;
```

### Fonctions fléchées

Les fonctions fléchées supportent les mêmes fonctionnalités que les fonctions anonymes, à l'exception que l'utilisation des variables de la portée parente est automatique.

```php
$fn1 = fn($x) => $x + $y;
```

### Variables globales

Le mot-clé global est utilisé pour lier une variable de la portée globale dans une portée locale. Une deuxième méthode pour accéder aux variables globales est d'utiliser le tableau associatif pré-défini `$GLOBALS`.

```php
$a = 1;
$b = 2;
function somme() {
    global $a, $b;
    $b = $a + $b;
}
somme();
echo $b;
```

### Variables statiques

Une variable statique a une portée locale uniquement, mais elle ne perd pas sa valeur lorsque le script appelle la fonction.

```php
function test()
{
    static $a = 0;
    echo $a;
    $a++;
}
```

Maintenant, la variable $a est initialisée uniquement lors du premier appel à la fonction et, à chaque fois que la fonction test() est appelée, elle affichera une valeur de $a incrémentée de 1.

### Variables dynamiques

Une variable dynamique prend la valeur d'une variable et l'utilise comme nom d'une autre variable.

```php
$a = 'bonjour';             // $a avec comme valeur "bonjour"
$$a = 'monde';              // $bonjour avec comme valeur "monde"
```

## Variables superglobales

Les variables internes qui sont toujours disponibles, quel que soit le contexte.

- `$GLOBALS` : Référence toutes les variables disponibles dans un contexte global
- `$_SERVER` : Variables de serveur et d'exécution
- `$_GET` : Variables de chaîne de requête
- `$_POST` : Données de formulaire depuis des requêtes HTTP POST
- `$_FILES` : Variable de téléchargement de fichier via HTTP
- `$_COOKIE` : Cookies HTTP
- `$_SESSION` : Variables de session
- `$_REQUEST` : Variables de requête HTTP
- `$_ENV` : Variables d'environnement

https://www.php.net/manual/fr/language.variables.superglobals.php

## Classes

```php
class SimpleClass
{
    // déclaration d'une propriété
    public $var = 'une valeur par défaut';

    // déclaration des méthodes
    public function displayVar() {
        echo $this->var;
    }
}
```

La pseudo-variable `$this` est disponible lorsqu'une méthode est appelée depuis un contexte objet. `$this` est la valeur de l'objet appelant.

es méthodes et propriétés peuvent aussi être accédés avec l'opérateur "nullsafe": ?->

```php
$result = $repository?->getUser(5)?->name;
```

Le mot-clé `final` empêche les classes enfants de redéfinir une méthode, une propriété ou constante en préfixant la définition avec `final`. Si la classe elle-même est définie comme finale, elle ne pourra pas être étendue.

```php
class BaseClass {
   public function test() {
       echo "BaseClass::test() appelée\n";
   }
   
   final public function moreTesting() {
       echo "BaseClass::moreTesting() appelée\n";
   }
}
```

### Constructeur

PHP permet aux développeurs de déclarer des constructeurs pour les classes. Les classes qui possèdent une méthode constructeur appellent cette méthode à chaque création d'une nouvelle instance de l'objet, ce qui est intéressant pour toutes les initialisations dont l'objet a besoin avant d'être utilisé.

```php
class BaseClass {
    function __construct() {
        print "Dans le constructeur de BaseClass\n";
    }
}
```

### Abstraction de classes

PHP a des classes, méthodes et propriétés abstraites. Les classes définies comme abstraites ne peuvent pas être instanciées, et toute classe contenant au moins une méthode abstraite doit elle-aussi être abstraite.

```php
abstract class AbstractClass 
{
    // Force les classes filles à définir cette méthode
    abstract protected function getValue();
    abstract protected function prefixValue($prefix);

    // méthode commune
   public function printOut()
   {
        print $this->getValue() . "\n";
   }
}
```

## Énumérations

```php
enum Suit
{
    case Hearts;
    case Diamonds;
    case Clubs;
    case Spades;
}
```

## Interfaces

Les interfaces d'objets permettent de créer du code qui spécifie quelles méthodes et propriétés une classe doit implémenter, sans avoir à définir comment ces méthodes ou propriétés sont implémentées.

```php
interface I
{
    // Une classe implémentant cette interface DOIT avoir une propriété publiquement lisible,
    // mais que celle-ci soit ou non modifiable publiquement n'est pas restreint.
    public string $readable { get; }

    // Une classe implémentant cette interface DOIT avoir une propriété publiquement modifiable,
    // mais que celle-ci soit ou non lisible publiquement n'est pas restreint.
    public string $writeable { set; }

    // Une classe implémentant cette interface DOIT avoir une propriété qui est à la fois publiquement
    // lisible et publiquement modifiable.
    public string $both { get; set; }
}
```

### Traits

Les traits sont un mécanisme de réutilisation de code dans un langage à héritage simple tel que PHP.

```php
trait TraitA {
    public function sayHello() {
        echo 'Hello';
    }
}

class MyHelloWorld
{
    use TraitA;

    public function sayHelloWorld() {
        $this->sayHello();
        echo "!\n";
    }
}
```

## Types

En PHP, chaque expression a l'un des types intégrés suivants en fonction de sa valeur:

- `null` : Le type null est le type unité de PHP, c'est-à-dire qu'il n'a qu'une seule valeur: `null`.
- `bool` : Le type bool ne possède que deux valeurs, et est utilisé pour exprimer une valeur de vérité. Il peut être soit `true` soit `false`.
- `int` : Un entier est un nombre appartenant à l'ensemble ℤ = {..., -2, -1, 0, 1, 2, ...}.
- `float` : nombre à virgule flottante
- `string`
- `array` => `dict`
- `object`
- `callable`
- `resource`
- `mixed` : accepte toutes les valeurs
- `void` : est une déclaration de type de retour uniquement, indiquant que la fonction ne retourne pas de valeur, mais que la fonction peut quand même se terminer.
- `never` : never est uniquement un type de retour indiquant que la fonction ne se termine pas.

### Types de classes relatives

- `self` : La valeur doit être une instance de la même classe que celle dans laquelle la déclaration de type est utilisée.
- `parent` : La valeur doit être une instance d'un parent de la classe dans laquelle la déclaration de type est utilisée.
- `static` : static est un type de retour uniquement qui exige que la valeur retournée soit une instance de la même classe que celle sur laquelle la méthode est appelée.

### Type cast

Le casting de type converti la valeur à un type donnée en écrivant le type entre parenthèse avant la valeur à convertir.

- `(int)` - cast en int
- `(bool)` - cast en bool
- `(float)` - cast en float
- `(string)` - cast en string
- `(array)` - cast en array
- `(object)` - cast en object
- `(unset)` - cast en NULL

## Fonctions utiles

- `array_filter` : Filtre les éléments d'un tableau grâce à une fonction de rappel
- `array_find` : Retourne le premier élément validant la fonction de rappel
- `array_map` : Applique une fonction sur les éléments d'un tableau
- `explode` : Scinde une chaîne de caractères en segments
- `htmlspecialchars` : Convertit les caractères spéciaux en entités HTML
- `is_null` : Indique si une variable vaut null
- `isset` : Détermine si une variable est déclarée et est différente de null
- `nl2br` : Insère un retour à la ligne HTML à chaque nouvelle ligne
- `str_contains` : Détermine si une chaîne contient une sous-chaîne donnée
- `urlencode` : Encode une chaîne en URL
- `var_dump` : Affiche les informations d'une variable
