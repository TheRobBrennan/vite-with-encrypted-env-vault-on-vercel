# Welcome

Let's deploy a Vite app with an encrypted `.env.vault` file to Vercel as suggested by [Deploy a Vite App to Vercel](https://www.dotenv.org/docs/frameworks/vite/vercel)

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
