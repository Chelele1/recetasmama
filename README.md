# Chela’s Recipe Book

An MIT-licensed, private recipe organizer inspired by the recipe-book workflow. This project is independent of Paprika and does not use its source, branding, or assets.

## Features

- Create, edit, and delete recipes.
- Categories: Breads, Salads, Meat, Fish, Chicken, Pasta, Desserts, Other.
- Search names, ingredients, and notes; mark favorites.
- Store ingredients, instructions, notes, servings, cooking time, and source.
- Attach JPG, PNG, or WebP photos up to 5 MB.
- Access the same collection on phone and computer after signing in.
- Download recipe text as JSON. This export excludes photo files and is a text copy; restoring exports is not implemented yet.

## Runtime and deployment

This first version uses React with Vinext, Cloudflare Workers, D1 for recipe records, R2 for photos, and Sites-provided sign-in. It is open-source application code, but the current authentication and deployment integration uses ChatGPT Sites. GitHub Pages alone cannot run its private storage backend. Deploying outside Sites requires an authentication adapter that verifies identity server-side; never trust arbitrary user-supplied identity headers.

Install dependencies with the package manager specified in package.json. The lockfile is included. Run `pnpm db:generate` after modifying `db/schema.ts`, `pnpm dev` for development, and `pnpm build` for a Worker build. D1 and R2 are declared as DB and BUCKET in `.openai/hosting.json`. Schema migrations are in `drizzle/`. Local development requires configured Cloudflare emulation and identity; there is no anonymous write fallback.

The deployed app checks the authenticated user on every API operation. Recipes are filtered by owner; photos use per-user keys. Recipe content is not committed to this repository.

## Current scope

Recipes are typed or pasted manually. Website extraction, grocery lists, meal planning, automatic quantity scaling, and offline mode are not implemented. The collection is private; the code can be public. This is a first functional version rather than full Paprika feature parity.

## License

MIT; see LICENSE.
