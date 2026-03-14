# node-sea-boilerplate

Boilerplate project for Node.js [single executable applications][node-sea]

[node-sea]: https://nodejs.org/api/single-executable-applications.html

## How to use

Write your code in `src/main.ts`.

### lint (biome) & type-checking (tsc)

```bash
npm run check
```

### Run code without build (for debug)

```bash
node src/main.ts
```

### Build

Your app will be stored in `build/app`.

```bash
npm run build
```

## What changed from the default

### Enabled correctness/useImportExtensions

To ensure we have `.ts` for every import.

```diff
diff --git a/biome.json b/biome.json
index 8d47a1e..9e70f08 100644
--- a/biome.json
+++ b/biome.json
@@ -15,7 +15,10 @@
        "linter": {
                "enabled": true,
                "rules": {
-                       "recommended": true
+                       "recommended": true,
+                       "correctness": {
+                               "useImportExtensions": "error"
+                       }
                }
        },
        "javascript": {
```

### Enabled noEmit

Since we only use TypeScript to perform type checking.
Type stripping, bundling, and minification are all done by esbuild.

```diff
diff --git a/tsconfig.json b/tsconfig.json
index 32f805d..6042987 100644
--- a/tsconfig.json
+++ b/tsconfig.json
@@ -3,6 +3,9 @@
     "@tsconfig/node24/tsconfig.json",
     "@tsconfig/node-ts/tsconfig.json",
   ],
+  "compilerOptions": {
+    "noEmit": true,
+  },
   "include": [
     "src/",
   ],
```

## Notes

- Currently, this project only supports the Linux x64 platform.
  But Node SEA also seems to work on other platforms like Windows x64 or macOS arm64.
- If you have problems with SIGSEGV, you may be using a stripped version of the Node.js binary.
  Node SEA seems not to work when symbols are stripped.
