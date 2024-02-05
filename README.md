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
