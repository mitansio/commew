# Local Development Environment Setup Guide

This is a development environment setup guide for contributors.

While environment setup is possible on Windows, this document is written for Mac OS.

## Node.js Installation

Please use the latest version of the 18.x series.

Since you may use different Node.js versions across multiple projects, it's recommended to set up version management for Node.js itself.

Here's an example setup using [asdf](https://asdf-vm.com):

```bash
asdf install nodejs 18.15.0

asdf local nodejs 18.15.0
```

Of course, you can use other version management tools without any issues.

The reason for using the 18.x series (with vague notation) is because [Vercel](https://vercel.com), which hosts this application, uses Node.js version 18.x.

Since there's no clear documentation about which minor version is being used, we're taking the approach of using the latest version in the 18.x series.

## Installing Dependencies

Once `node -v` shows the desired version, run the following command:

Use `npm ci` to install dependency packages.

## Environment Variables Configuration

Place a `.env` file in the project root with the following content:

```
GOOGLE_OIDC_CLIENT_ID=Google OpenID Connect Client ID
GOOGLE_OIDC_CLIENT_SECRET=Google OpenID Connect Client Secret
NEXTAUTH_URL=http://localhost:5656
NEXTAUTH_SECRET=sufficiently long string
BACKEND_API_BASE_URL=http://127.0.0.1:5757
API_BASIC_AUTH_USER=Refer to Vercel values
API_BASIC_AUTH_PASSWORD=Refer to Vercel values
NEXT_PUBLIC_GOOGLE_TAG_MANAGER_ID=Not required, but refer to Vercel values if you want to debug GA etc.
NEXT_PUBLIC_APP_URL=http://localhost:5656
```

Some environment variables contain sensitive information and cannot be documented directly, so please refer to [Vercel's environment variables settings](https://vercel.com/commew/timelogger-web/settings/environment-variables) directly.

### If manually setting environment variables is tedious

If you have the `vercel` command available, you can run `vercel env pull .env.local` to expand environment variables into your local `.env` file.

- https://vercel.com/docs/cli
- https://nextjs-ja-translation-docs.vercel.app/docs/basic-features/environment-variables

## Starting the Development Server

Run `npm run dev`.

You can access the application at the following URL:

http://localhost:5656

# npm Script Explanations

## Build

Run `npm run build` to execute Next.js Build command.

While you rarely use this during local development, if this build fails, the CI will fail.

## Start

Run `npm run start` to start the server based on the built source code.

The application server running on [Vercel](https://vercel.com) is also executed using this command.

Since hot reload doesn't work, you rarely use this for local development.

## Linter

Run `npm run lint` to execute the Linter.

If errors remain here, the CI will fail.

## Formatter

Run `npm run format` to format the source code.

Linter errors can be automatically fixed to some extent using this command.

## Test

Run `npm run test` to execute test code.

## Starting Storybook

Run `npm run storybook`.

You can access it at `http://localhost:6006`.

Component behavior verification is basically done on this Storybook.

## Outputting Storybook as Static HTML Files

Run the following command:

```bash
npm run build-storybook
```

You can confirm that HTML files are output to the `storybook-static/` directory.

You can view Storybook by opening `index.html` in a browser.

Incidentally, deployments to [chromatic](https://www.chromatic.com/builds?appId=63d52217f1430a5ad69846cd) are made for each commit.

As mentioned in the README, you can view the latest Storybook from the following URL:

https://main--63d52217f1430a5ad69846cd.chromatic.com

## Starting OpenAPI MockServer

Run the following command to start on port `5757`:

```bash
npm run api-mock:start
```

Here's an example request using the `curl` command:

```bash
curl -v \
-X POST \
-H "Prefer: code=201, example=ExampleSuccess" \
-H "Content-Type: application/json" \
-H "Authorization: Basic YWRtaW5Vc2VyOnBhc3N3b3JkMTIzNA==" \
-d '
{
  "sub": "99999999999999999999999999999",
  "provider": "google"
}
' \
http://127.0.0.1:5757/accounts | jq
```

While test code uses [msw](https://mswjs.io/) for mocking, during development you can use this MockServer to verify the same behavior as the actual API.

Please note the `Prefer` Header being sent.

By sending this Header, you can obtain the intended response result.

For example, to get an authentication error response for `POST /accounts`, make the request as follows:

```bash
curl -v \
-X POST \
-H "Prefer: code=401, example=ExampleUnAuthenticated" \
-H "Content-Type: application/json" \
-H "Authorization: Basic YWRtaW5Vc2VyOnBhc3N3b3JkMTIzNA==" \
-d '
{
  "sub": "99999999999999999999999999999",
  "provider": "google"
}
' \
http://127.0.0.1:5757/accounts | jq
```

For more details, please refer to the official documentation:

https://meta.stoplight.io/docs/prism/beeaad4dc0227-prism-cli#modifying-responses

## Generating Type Definitions from OpenAPI Configuration Files

Running the command `npm run generate:schema` will generate type definitions in `src/types/schema.ts`.

If you modify `public/docs/api/openapi.yaml` in the API design, please run this command to update the type definitions and commit the changes.
