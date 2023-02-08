# Building Worker with D1 and Nuxt 3

### Overview:

Worker cannot be built with D1 bindings and Nuxt 3.

1. Nuxt 3 built & deployed to Workers - success.
2. Nuxt 3 with KV bindings built & deployed to Workers - success.
3. Nuxt 3 with D1 bindings **cannot** be run in `dev` or `publish`ed.

Nuxt builds fine with the `cloudflare` Nitro preset. 

KV bindings work AOK, however, D1 doesn't but I'd have expected similar behaviour.

### Error:

```
✘ [ERROR] No matching export in ".output/server/index.mjs" for import "default"

    ../../../../../private/var/folders/6c/6l0q50813qd2t24z8zztts2r0000gn/T/tmp-2814-oylSIpoFBDZf/d1-beta-facade.entry.js:5:7:
      5 │ import worker, * as OTHER_EXPORTS from "/Users/me/src/templates...
        ╵        ~~~~~~


✘ [ERROR] Build failed with 1 error:

  ../../../../../private/var/folders/6c/6l0q50813qd2t24z8zztts2r0000gn/T/tmp-2814-oylSIpoFBDZf/d1-beta-facade.entry.js:5:7:
  ERROR: No matching export in ".output/server/index.mjs" for import "default"

```

### Steps to Reproduce:

1. Create a Nuxt project.
2. Create a Wrangler project.
3. Integrate the two - clone the repo [here](https://github.com/smcstewart/nuxt3-workers-d1) already setup.
4. Run `npm install`.
5. Run `wrangler kv:namespace create tester`.
6. Run `wrangler d1 create tester`.
7. Use your Cloudflare Account ID along with the IDs generated from the `wrangler` commands to update the `wrangler.toml` file's bindings of D1 and KV.
8. Run `wrangler dev` or `wrangler publish` and you get the error.
9. Comment out the D1 bindings line and re-run `wrangler dev` or `wrangler publish` and the error no longer exists.
