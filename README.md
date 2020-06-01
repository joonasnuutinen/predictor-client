[![Build Status](https://travis-ci.com/joonasnuutinen/ennustin-client.svg?branch=master)](https://travis-ci.com/joonasnuutinen/ennustin-client)

Ennustin is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/zeit/next.js/tree/canary/packages/create-next-app).

## Configuring Auth0

1. Go to the [Auth0 dashboard](https://manage.auth0.com/) and create a new application of type _Regular Web Applications_ and make sure to configure the following
2. Go to the settings page of the application
3. Configure the following settings:

- _Allowed Callback URLs_: Should be set to `http://localhost:3000/api/callback` when testing locally or typically to `https://myapp.com/api/callback` when deploying your application.
- _Allowed Logout URLs_: Should be set to `http://localhost:3000/` when testing locally or typically to `https://myapp.com/` when deploying your application.

4. Save the settings

### Configuring Next.js

In the Next.js configuration file (`next.config.js`) you'll see that different environment variables are being assigned.

### Local Development

For local development you'll want to create a `.env` file with the necessary settings.

The required settings can be found on the Auth0 application's settings page:

```
AUTH0_DOMAIN=YOUR_AUTH0_DOMAIN
AUTH0_CLIENT_ID=YOUR_AUTH0_CLIENT_ID
AUTH0_CLIENT_SECRET=YOUR_AUTH0_CLIENT_SECRET

SESSION_COOKIE_SECRET=viloxyf_z2GW6K4CT-KQD_MoLEA2wqv5jWuq4Jd0P7ymgG5GJGMpvMneXZzhK3sL (at least 32 characters, used to encrypt the cookie)

REDIRECT_URI=http://localhost:3000/api/callback
POST_LOGOUT_REDIRECT_URI=http://localhost:3000/
```

### Hosting on Vercel

When deploying this example to Vercel you'll want to update the `now.json` configuration file.

```json
{
  "build": {
    "env": {
      "AUTH0_DOMAIN": "YOUR_AUTH0_DOMAIN",
      "AUTH0_CLIENT_ID": "YOUR_AUTH0_CLIENT_ID",
      "AUTH0_CLIENT_SECRET": "@auth0_client_secret",
      "REDIRECT_URI": "https://my-website.now.sh/api/callback",
      "POST_LOGOUT_REDIRECT_URI": "https://my-website.now.sh/",
      "SESSION_COOKIE_SECRET": "@session_cookie_secret",
      "SESSION_COOKIE_LIFETIME": 7200
    }
  }
}
```

- `AUTH0_DOMAIN` - Can be found in the Auth0 dashboard under `settings`.
- `AUTH0_CLIENT_ID` - Can be found in the Auth0 dashboard under `settings`.
- `AUTH0_CLIENT_SECRET` - Can be found in the Auth0 dashboard under `settings`.
- `REDIRECT_URI` - The url where Auth0 redirects back to, make sure a consistent url is used here.
- `POST_LOGOUT_REDIRECT_URI` - Where to redirect after logging out
- `SESSION_COOKIE_SECRET` - A unique secret used to encrypt the cookies, has to be at least 32 characters. You can use [this generator](https://generate-secret.now.sh/32) to generate a value.
- `SESSION_COOKIE_LIFETIME` - How long a session lasts in seconds. The default is 2 hours.

The `@auth0_client_secret` and `@session_cookie_secret` are [Vercel environment secrets](https://vercel.com/docs/v2/environment-variables-and-secrets/)

You can create the `@auth0_client_secret` by running:

```
now secrets add auth0_client_secret PLACE_YOUR_AUTH0_CLIENT_SECRET
```

And create the `session_cookie_secret` by generating a value [here](https://generate-secret.now.sh/32) and running:

```
now secrets add session_cookie_secret PLACE_YOUR_SESSION_COOKIE_SECRET
```

## Running the development server

First, run the development server:

```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.js`. The page auto-updates as you edit the file.
