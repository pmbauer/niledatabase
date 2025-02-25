# Multi-tenant todo list app with Nile and NextJS 13

This template shows how to use Nile with NextJS 13 for a multi-tenant todo list application.

- [Live demo](https://nextjs-quickstart-omega.vercel.app)
- [Video guide - TBD](TBD)
- [Step by step guide](https://niledatabase-www.vercel.app/docs/getting-started/languages/nextjs)

## Getting Started

### 1. Create a new database

Sign up for an invite to [Nile](https://thenile.dev) if you don't have one already and choose "Yes, let's get started". Follow the prompts to create a new workspace and a database.

### 2. Create todo table

After you created a database, you will land in Nile's query editor. Since our application requires a table for storing all the "todos" this is a good time to create one:

```sql
    create table todos (id uuid, tenant_id uuid, title varchar(256), complete boolean);
```

If all went well, you'll see the new table in the panel on the left hand side of the query editor. You can also see Nile's built-in tenant table next to it.

### 3. Getting credentials

In the left-hand menu, click on "Settings" and then select "Credentials". Generate credentails and keep them somewhere safe. These give you access to the database.

### 4. Setting the environment

If you haven't cloned this repository yet, now will be an excellent time to do so.

```bash
git clone https://github.com/niledatabase/niledatabase
cd niledatabase/examples/quickstart/nextjs
```

Rename `.env.local.example` to `.env.local`, and update it with your workspace and database name.
_(Your workspace and database name are displayed in the header of the Nile dashboard.)_
Also fill in the username and password with the credentials you picked up in the previous step.

It should look something like this:

```bash
# Client (public) env vars

# the URL of this example + where the api routes are located
# Use this to instantiate Nile context for client-side components
NEXT_PUBLIC_BASE_PATH=http://localhost:3000/api
NEXT_PUBLIC_WORKSPACE=todoapp_demo
NEXT_PUBLIC_DATABASE=demo_db_nextjs_qs

# Private env vars that should never show up in the browser
# These are used by the server to connect to Nile database
NILE_DB_HOST = "db.thenile.dev"
NILE_USER = "018ad484-0d52-7274-8639-057814be60c3"
NILE_PASSWORD = "0d11b8e5-fbbc-4639-be44-8ab72947ec5b"

# The URL of the Nile API
# Use this to instantiate Nile Server context for server-side use of the "api" SDK
NEXT_PUBLIC_NILE_API=https://api.thenile.dev 

# Uncomment if you want to try Google Auth
# AUTH_TYPE=google
```

Install dependencies with `yarn install` or `npm install`.

### 5. Running the app

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

If all went well, your browser should show you the first page in the app, asking you to login or sign up.

After you sign up as a user of this example app, you'll be able to see this user by going back to Nile Console and running `select * from users` in the query editor.

Login with the new user, and you can create a new tenant and add tasks for the tenant. You can see the changes in your Nile database by running

```sql
select name, title, complete from
tenants join todos on tenants.id=todos.tenant_id
```

## Learn More

To learn more about how this example works and how to use Nile:
- [In depth explanation of this example](https://niledatabase-www.vercel.app/docs/getting-started/languages/nextjs)
- [More about tenants in Nile](https://niledatabase-www.vercel.app/docs/tenant-management)
- [More on user authentication with Nile](https://niledatabase-www.vercel.app/docs/user-authentication)
- [Nile's Javascript SDK reference](https://niledatabase-www.vercel.app/docs/reference/sdk-reference)

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.
