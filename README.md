# Welcome

Let's deploy a Vite app with an encrypted `.env.vault` file to Vercel as suggested by [Deploy a Vite App to Vercel](https://www.dotenv.org/docs/frameworks/vite/vercel)

The [demo](https://vite-with-encrypted-env-vault-on-vercel.vercel.app) for this repo can be viewed at [https://vite-with-encrypted-env-vault-on-vercel.vercel.app](https://vite-with-encrypted-env-vault-on-vercel.vercel.app).

## Getting started

### Initial setup

First, let's create our [Vite](https://vitejs.dev) application:

```sh
% npm create vite@latest .

✔ Current directory is not empty. Please choose how to proceed: › Ignore files and continue
✔ Select a framework: › Vanilla
✔ Select a variant: › TypeScript

Done. Now run:

  npm install
  npm run dev

```

After we have run the `npm install` command, let's run `npm run dev` to view our application:

```sh
# Install our dependencies
% npm install

# Start our development server
% npm run dev
VITE v5.0.12  ready in 134 ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
  ➜  press h + enter to show help
```

In the above example, we should be able to open our favorite web browser and navigate to [http://localhost:5173](http://localhost:5173) 🎉

Once we've verified our local development environment is up and running, it's time to do the initial deployment to Vercel:

```sh
% npx vercel@latest deploy --prod
Need to install the following packages:
vercel@33.4.1
Ok to proceed? (y) 
npm WARN deprecated fsevents@2.1.3: "Please update to latest v2.3 or v2.2"
npm WARN deprecated debug@4.1.1: Debug versions >=3.2.0 <3.2.7 || >=4 <4.3.1 have a low-severity ReDos regression when used in a Node.js environment. It is recommended you upgrade to 3.2.7 or 4.3.1. (https://github.com/visionmedia/debug/issues/797)
npm WARN deprecated uuid@3.3.2: Please upgrade  to version 7 or higher.  Older versions may use Math.random() in certain circumstances, which is known to be problematic.  See https://v8.dev/blog/math-random for details.
Vercel CLI 33.4.1
? Set up and deploy “~/repos/vite-with-encrypted-env-vault-on-vercel”? [Y/n] y
? Which scope do you want to deploy to? TheRobBrennan
? Link to existing project? [y/N] n
? What’s your project’s name? vite-with-encrypted-env-vault-on-vercel
? In which directory is your code located? ./
Local settings detected in vercel.json:
Auto-detected Project Settings (Vite):
- Build Command: vite build
- Development Command: vite --port $PORT
- Install Command: `yarn install`, `pnpm install`, `npm install`, or `bun install`
- Output Directory: dist
? Want to modify these settings? [y/N] n
🔗  Linked to therobbrennan/vite-with-encrypted-env-vault-on-vercel (created .vercel and added it to .gitignore)
🔍  Inspect: https://vercel.com/therobbrennan/vite-with-encrypted-env-vault-on-vercel/7vV9eP7u7NKmvLRSsLq1BiXDjQgF [1s]
✅  Production: https://vite-with-encrypted-env-vault-on-vercel-f82di0bfa-therobbrennan.vercel.app [1s]

```

After successfully deploying to Vercel, my project is available at [https://vite-with-encrypted-env-vault-on-vercel.vercel.app](https://vite-with-encrypted-env-vault-on-vercel.vercel.app).

Once your app is deployed to Vercel, it will say `Hello, undefined.` because it doesn't have access to the `VITE_HELLO` environment variable yet. We'll configure that in the next section.

### Environment variables

First, let's define our environment variables. As part of standard programming practice, it's helpful if your project has a `.env.example` file to help get users started and understand what environment variables and other services or integrations need to be defined for your application to work.

Please copy `.env.sample` to `.env`:

```sh
% cp .env.sample .env
```

Next, install `dotenv` so that our environment variables from `.env` are injected into our Vite application:

```sh
% npm install dotenv --save # Requires dotenv >= 16.1.0
```

If we run our development server with `npm run dev` we should see our "Hello World." message at [http://localhost:5173](http://localhost:5173) 🎉

#### Build .env.vault

If this is your first time setting up a `dotenv-vault`, please follow these instructions:

```sh
# Create a new .env.vault
% npx dotenv-vault@latest new

# Follow the prompts to create a new vault/account

# Confirm your dotnet-vault account by clicking on the verification link that was emailed to you

# Login to dotenv-vault
% npx dotenv-vault@latest login

# Open dotenv-vault
% npx dotenv-vault@latest open

```

Once you have a vault created for `dotnet-vault` you will want to push your `.env` file so that those changes are automatically pushed to the vault.

```sh
# Push your latest .env file changes
% npx dotenv-vault@latest push

# OPTIONAL: Open and edit your production vault
% npx dotenv-vault@latest open production

```

Update `VITE_HELLO` in production so it has a value of "production" (without quotes).

Build your `.env.vault` file - which **CAN AND SHOULD BE COMMITTED TO SOURCE CONTROL**:

```sh
% npx dotenv-vault@latest build

remote:   Securely building .env.vault... done
remote:   Securely built .env.vault

Next:
1. Commit .env.vault to code
2. Set DOTENV_KEY on server
3. Deploy your code

(run npx dotenv-vault@latest keys to view DOTENV_KEYs)

```

#### Configure Vercel to use your dotnet-vault

The last step will be in obtaining your production `DOTENV_KEY` from your `dotenv-vault` and add that to Vercel as a new `DOTENV_KEY` environment variable for deployment:

```sh
# Fetch your production DOTENV_KEY
% npx dotenv-vault@latest keys production
remote:   Listing .env.vault decryption keys... done
dotenv://:key_1234@dotenv.org/vault/.env.vault?environment=production

# Set DOTENV_KEY on Vercel using the CLI
% npx vercel@latest env add DOTENV_KEY
Vercel CLI 33.4.1
? What’s the value of DOTENV_KEY? dotenv://:key_1234@dotenv.org/vault/.env.vault?environment=production
? Add DOTENV_KEY to which Environments (select multiple)? Production, Preview, Development
✅  Added Environment Variable DOTENV_KEY to Project vite-with-encrypted-env-vault-on-vercel [229ms]

# Build and deploy to Vercel using the latest production secrets
% npx vercel@latest deploy --prod

```

¡Voila! All the environment variables this application uses can be managed and maintained in the `dotenv-vault`, with Vercel only needing to be aware of the `DOTENV_KEY` environment variable.
