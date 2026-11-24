# Terna Electricity Data API

Terna's public APIs provide access to electricity data for Italy. This guide explains how to obtain an access token and use it to request actual generation data.

## Register an application

1. Create an account on the [Terna developer portal](https://developer.terna.it/) and confirm your email address.
2. Sign in and go to **My Account → Applications**.
3. Select **Create a new App**, choose a name without personal information, and leave the **Public** package selected. Accept the terms and register the application.
4. On the application page, find the **Key** (`client_id`) and **Secret** (`client_secret`).

See Terna's [application registration guide](https://developer.terna.it/docs/read/How_to_register_an_application) for details.

## Obtain an access token

Use the application credentials to request a token:

```bash
curl -X POST https://api.terna.it/public-api/access-token \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "client_id=MY_KEY" \
  -d "client_secret=MY_SECRET" \
  -d "grant_type=client_credentials"
```

Replace `MY_KEY` and `MY_SECRET` with your application's credentials. Keep the secret private and do not send these credentials in data request headers.

The access token expires after 300 seconds. Request a new token when it expires.

## Request electricity data

Use the access token as a bearer token. For example, to request actual generation data for April 23, 2022:

```bash
curl --location --request GET \
  'https://api.terna.it/generation/v2.0/actual-generation?dateFrom=23/04/2022&dateTo=23/04/2022' \
  --header 'Authorization: Bearer MY_TEMPORARY_TOKEN'
```

Replace `MY_TEMPORARY_TOKEN` with the access token returned by the token request. Adjust `dateFrom` and `dateTo` to request another date range.