Builder drops file extension when js module is imported from jsx module.
===

This project illustrates **SystemJS Build Tool 0.14.11** [issue #413](https://github.com/systemjs/builder/issues/413).

There is a package `test-app` that sits in `lib` folder and consists of two modules `main.jsx` and `module.js`. Module `module.js` is imported into `main.jsx` module. In development mode (files are loaded separately to browser) SystemJS loads both modules as expected with correct extensions.

During build of self-executing bundle SystemJS builder is looking for `lib/module` file instead of `lib/module.js`. It is only reproducible when both `defaultExtension: false` option is set **and**  path to package is specified in `paths` option. Particularly, when renaming `lib` folder to `test-app` and removing its entry from `paths` build passes successfully. 

Pay attention that **SystemJS** and **SystemJS Build Tool** both work with the same configuration, but first handles it correctly and second fails.

Usage of this example
---

### 1. Install application:

  ```
    npm install
  ```

### 2. Launch development server:

  ```
    npm start
  ```

Open `http://localhost:9001` in browser. Everything works fine in development mode. 

### 3. Launch build:

  ```
    npm run build
  ```

It should create a self-executing bundle... but SystemJS builder fails with `ENOENT` error :(

In case error is fixed, continue to next step.

### 4. Launch production server:

  ```
    npm run prod
  ```

Open `http://localhost:9009` in browser. Output should be the same as on step 2.
