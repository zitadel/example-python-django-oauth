# Example Python Django with external OAUTH Provider for an API

This repository provides a Django example for ZITADEL using OAuth to provide the API with security through permission from an external system.
This example is provided as companion to our [guide](https://zitadel.com/docs/examples/secure-api/django),
which should produce this application when followed.

## Features

- OAuth integration trought introspection calls
- Permission checks on user roles on API calls
- Public page at `/public`
- Authorized `/private` page for all users.
- Authorized `/private-scoped` page for all users with `read:messages` role

## Getting started

If you want to run this example directly you can fork and clone it to your system.
Be sure to [configure ZITADEL](https://docs-git-docs-example-symfony-zitadel.vercel.app/docs/examples/login/symfony#zitadel-setup) to accept requests from this app.

### Prerequisites

Create a project as described in [Secure an API using the JSON Web Token Profile in ZITADEL](https://github.com/zitadel/examples-api-access-and-token-introspection/blob/main/api-jwt/README.md).

You should have a key-file `.json`, the domain ZITADEL is running under and the token and introspection URL.

Create an serviceuser as descirbed in [Call a Secured API Using JSON Web Token (JWT) Profile](https://github.com/zitadel/examples-api-access-and-token-introspection/tree/main/service-user-jwt).

You should have a client-key-file `.json` and the ID of the project you gave permissons to.

You have to install Python as described in [their documentation](https://wiki.python.org/moin/BeginnersGuide/Download) and then download all dependencies through:

```bash
python -m pip install -r requirements.txt
```

Alternatively if you have a system with Docker and an IDE capable of running [Development Container](https://containers.dev/),
definitions are provided with a complete Python environment, configuration and tools required for Django development.
Use your IDE to build and launch the development environment or use GitHub code spaces from your browser.

### Django

After setting up your system and repository, create the sqlite-database.

```bash
python manage.py migrate
```

And run the server:

```bash
python manage.py runserve
```

Visit [http://localhost:8000/public/] to see if the server is running correctly.