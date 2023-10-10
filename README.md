Simple example library to reproduce error when using bun with a native module, `webbluetooth`.

1. Inside the `my-lib` directory we install dependencies and then build the `my-lib` module using `bun build ./src/index.ts --target=node --outdir dist`
2. Then we link it using `bun link`
3. Next we move over to the `examples/cli` app, link `my-lib` using `bun link my-lib` and then install dependencies
4. Finally we run `bun run src/index.ts --verbose` and get `error: Could not locate the bindings file.` (see below)

```bash
➜ cli bun run src/index.ts --verbose
340 |         if (e.code !== "MODULE_NOT_FOUND" && e.code !== "QUALIFIED_PATH_RESOLUTION_FAILED" && !/not find/i.test(e.message)) {
341 |           throw e;
342 |         }
343 |       }
344 |     }
345 |     err = new Error("Could not locate the bindings file. Tried:\n" + tries.map(function(a) {
              ^
error: Could not locate the bindings file. Tried:
 → /Users/olafur/dev/vite-lib/my-lib/build/simpleble.node
 → /Users/olafur/dev/vite-lib/my-lib/build/Debug/simpleble.node
 → /Users/olafur/dev/vite-lib/my-lib/build/Release/simpleble.node
 → /Users/olafur/dev/vite-lib/my-lib/out/Debug/simpleble.node
 → /Users/olafur/dev/vite-lib/my-lib/Debug/simpleble.node
 → /Users/olafur/dev/vite-lib/my-lib/out/Release/simpleble.node
 → /Users/olafur/dev/vite-lib/my-lib/Release/simpleble.node
 → /Users/olafur/dev/vite-lib/my-lib/build/default/simpleble.node
 → /Users/olafur/dev/vite-lib/my-lib/compiled/20.8.0/darwin/arm64/simpleble.node
 → /Users/olafur/dev/vite-lib/my-lib/addon-build/release/install-root/simpleble.node
 → /Users/olafur/dev/vite-lib/my-lib/addon-build/debug/install-root/simpleble.node
 → /Users/olafur/dev/vite-lib/my-lib/addon-build/default/install-root/simpleble.node
 → /Users/olafur/dev/vite-lib/my-lib/lib/binding/node-v115-darwin-arm64/simpleble.node
      at bindings (/Users/olafur/dev/vite-lib/my-lib/dist/index.js:345:10)
      at /Users/olafur/dev/vite-lib/my-lib/dist/index.js:439:18
      at /Users/olafur/dev/vite-lib/my-lib/dist/index.js:17:71
      at /Users/olafur/dev/vite-lib/my-lib/dist/index.js:593:20
      at /Users/olafur/dev/vite-lib/my-lib/dist/index.js:17:71
      at /Users/olafur/dev/vite-lib/my-lib/dist/index.js:1043:28
      at /Users/olafur/dev/vite-lib/my-lib/dist/index.js:17:71
      at /Users/olafur/dev/vite-lib/my-lib/dist/index.js:2527:19
      at /Users/olafur/dev/vite-lib/my-lib/dist/index.js:17:71
      at /Users/olafur/dev/vite-lib/my-lib/dist/index.js:2877:20
      at /Users/olafur/dev/vite-lib/my-lib/dist/index.js:17:71
      at /Users/olafur/dev/vite-lib/my-lib/dist/index.js:2886:34
```
