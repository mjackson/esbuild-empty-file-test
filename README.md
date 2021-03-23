This is a repro of what I think might be a bug in esbuild where it interprets an empty file as a module with a `default` export when it is imported via `import *`.

To reproduce:

- Make sure you have node 14 or newer (so you can run ESM w/out compiling anything)
- Run `b.mjs` with node:

```sh
$ node b.mjs
```

You should see the following console output:

```log
[Module] {  }
```

It's an empty module (no exports).

- Next, run install + esbuild:

```sh
$ npm install
$ esbuild --bundle --outfile=out.js b.mjs
```

- Now, run the esbuild output:

```sh
$ node out.js
```

You should see the following console output:

```log
{ default: {} }
```

The built module is an object with a single `default` export which is an empty object.
