# Propel

ORM de Thelia.

https://propelorm.org/documentation/

## CRUD

Instancier une Query :

```php
<?php
$firstAuthor = AuthorQuery::create();
```

Récupérer des champs :

```php
<?php
echo $author->getId();        // 1
echo $author->getFirstName(); // 'Jane'
echo $author->getLastName();  // 'Austen'
```

Récupérer une entrée depuis son ID :

```php
<?php
$firstAuthor = AuthorQuery::create()->findPK(1);
```

Récupérer plusieurs entrées depuis leurs IDs :

```php
<?php
$selectedAuthors = AuthorQuery::create()->findPKs(array(1,2,3,4,5,6,7));
```

Filtrer les entrées (renvoi tout par défaut) :

```php
<?php
$authors = AuthorQuery::create()->find();
```
