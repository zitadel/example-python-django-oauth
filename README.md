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
Be sure to [configure ZITADEL](https://zitadel.com/docs/examples/secure-api/django#zitadel-setup) to accept requests from this API.

### Prerequisites

You have to install Python as described in [their documentation](https://wiki.python.org/moin/BeginnersGuide/Download) and then download all dependencies through:

```bash
python -m pip install -r requirements.txt
```

Alternatively if you have a system with Docker and an IDE capable of running [Development Container](https://containers.dev/),
definitions are provided with a complete Python environment, configuration and tools required for Django development.
Use your IDE to build and launch the development environment or use GitHub code spaces from your browser.

### Django

Fill in the `.env`-file in your directory with the following information:

```bash
ZITADEL_INTROSPECTION_URL = 'URL to the introspection endpoint to verify the provided token'
ZITADEL_DOMAIN = 'Domain used as audience in the token verification'
API_PRIVATE_KEY_FILE_PATH = 'Path to the key.json created in ZITADEL'
```

It should look something like this:

```bash
ZITADEL_INTROSPECTION_URL = 'https://example.zitadel.cloud/oauth/v2/introspect'
ZITADEL_DOMAIN = 'https://example.zitadel.cloud'
API_PRIVATE_KEY_FILE_PATH = '/tmp/example/250719519163548112.json'
```

Run database migrations:

```bash
python manage.py migrate
```

And run the server:

```bash
python manage.py runserver
```

Visit [http://localhost:8000/api/public](http://localhost:8000/api/public) to see if the server is running correctly.
Then you can call [http://localhost:8000/api/private](http://localhost:8000/api/private) for example with CURL:

```bash
export TOKEN='eyJhbGciOiJSUzI1NiIsImtpZCI6IjI1MD...'
curl -H "Authorization: Bearer $TOKEN" -X GET http://localhost:8000/api/private
```
