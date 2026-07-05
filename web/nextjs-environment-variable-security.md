# Next.js Environment Variable Security

## Problem

In Next.js, environment variables are separated into server-only and browser-exposed. If sensitive secrets (API keys, database passwords) are inadvertently prefixed with NEXT_PUBLIC or loaded into the client bundle, they become visible in the browser.

## Symptoms

- Secrets appear in the browser's source code or network requests.
- Unexpected environment variables are accessible via `process.env` on the client.
- API credentials are accidentally leaked in the front-end.

## Investigation

In Next.js, environment variables that begin with `NEXT_PUBLIC_` or `NEXT_RUNTIME_` are exposed to the client bundle, while variables without these prefixes are server-only. I found that I accidentally prefixed a private key with `NEXT_PUBLIC_`, causing it to be bundled into the client code.

## Solution

- Keep sensitive variables (API keys, tokens) in `.env.local` without the `NEXT_PUBLIC_` prefix.
- Use `NEXT_PUBLIC_` only for variables meant for the browser (e.g., analytics IDs).
- Remove the `NEXT_PUBLIC` prefix from secrets and restart the development server to ensure the variable isn't exposed.
- Audit the build output with `next build` to ensure secrets are not included.

## Result

After removing the prefix from the sensitive variable and rebuilding the app, the secret no longer appears in the client bundle or network requests. Only non-sensitive IDs remain accessible through `process.env.NEXT_PUBLIC_*`.

## What I Learned

Next.js environment variable prefixes determine client vs server exposure. Always double-check your `.env` files and prefixes to avoid accidentally exposing secrets in the browser.
