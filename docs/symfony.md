# Symfony

## Structure

- `bin/` : The famous bin/console file lives here (and other, less important executable files).
- `config/` : Contains configuration. You will configure routes, services and packages.
- `public/` : This is the document root for your project: you put any publicly accessible files here.
- `templates/` : All your Twig templates live here.
- `src/` : All your PHP code lives here.
- `var/` : This is where automatically-created files are stored, like cache files (var/cache/) and logs (var/log/).
- `vendor/` : Third-party (i.e. "vendor") libraries live here! These are downloaded via the Composer package manager.

## Commandes utiles

- `php bin/console debug:router` : Liste toutes les routes
- `php bin/console lint:twig` : Vérifie les templates Twig
- `php bin/console debug:twig` : Liste les informations de Twig
- `php bin/console make:controller <nom>` : Crée un nouveau contrôleur