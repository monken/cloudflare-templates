# Template: worker-d1-api

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/cloudflare/templates/tree/main/worker-d1-api)

> **Note: requires D1 Open Alpha Access**

### Getting started

Next, run the following commands in the console:

```sh
git clone https://github.com/cloudflare/templates.git
cd worker-d1-api
npm install

# Make sure you've logged in
npx wrangler login

# Create the D1 Database
npx wrangler d1 create d1-api

# Add config to wrangler.toml as instructed

# Fill the DB with seed data from an SQL file:
npx wrangler d1 execute d1-api --file ./schemas/schema.sql

# Deploy the worker
npx wrangler publish
```

Then test out your new Worker!

### Developing locally

To develop on your worker locally, it can be super helpful to be able to copy down a copy of your production DB to work on. To do that with D1:

```sh
# Create a fresh backup on R2
npx wrangler d1 backup create d1-api

# Make sure you have the directory where wrangler dev looks for local D1
mkdir -p wrangler-local-state/d1

# Copy the `id` of the backup, and download the backup into that directory
npx wrangler d1 backup download d1-api <backup-id> --output ./wrangler-local-state/d1/DB.sqlite3

# Then run wrangler dev --local with persistence
npx wrangler dev --local --experimental-enable-local-persistence
```

**Note:** the local D1 development environment is under active development and may have some incorrect behavior. If you have issues, run `npm install wrangler@d1` to make sure you're on the latest version, or provide feedback in Discord.
