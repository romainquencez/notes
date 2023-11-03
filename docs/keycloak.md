# Keycloak

## Principe

### Realm

Un realm est un ensemble d'utilisateurs. Par défaut un realm `master` existe, mais est réservé à Keycloak et ne doit pas être utilisé par l'application.

## Authentification

Depuis le front de l'application, l'utilisateur souhaite se connecter. Il est redirigé vers le front de connexion de Keycloak, où il peut s'identifier mais aussi demander un nouveau mot de passe si il l'a oublié.

Une fois ses identifiants renseignés et envoyés, Keycloak redirige l'utilisateur vers une URL de l'application (callback). L'application a accès à un jeton de courte validité, qui doit être envoyé à Keycloak pour récupérer un jeton d'accès.

Ce jeton d'accès devra être inclus dans l'entête de chaque requête HTTP vers l'API de l'application. L'application peut utiliser une bibliothèque qui va se charger de vérifier la validité du jeton, et le cas échéant va tenter d'en générer un nouveau.

## Configuration

Un service Keycloak doit être créé.

Accéder à l'admin, et créer un nouveau realm.

* [Get started with Keycloak on Docker](https://www.keycloak.org/getting-started/getting-started-docker)
