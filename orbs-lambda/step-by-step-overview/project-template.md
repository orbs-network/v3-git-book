# Project Template

## Directory structure

Orbs Lambda enforces a strict directory structure for your project. It is recommended to create a [local fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) of the official Orbs Lambda repo on GitHub:

[https://github.com/orbs-network/orbs-lambda](https://github.com/orbs-network/orbs-lambda)

* The root of your project should contain a top-level directory with your [_unique ID_](select-unique-id.md)
* This directory should contain the file `index.js` - the main entry point of your lambda
* This directory may contain any additional dependencies (`.js` and `.json` files)
* This directory may contain a test suite under the `test` subdirectory
  * Test suite files should have the `.spec.js` suffix
  * The tests directory may contain any additional dependencies (`.js` and `.json` files)
* Any `package.json` files should be found in the root

## Setting up example

Assuming your local project working directory is `my-lambda-project`&#x20;

```
git clone https://github.com/orbs-network/orbs-lambda my-lambda-project
```

And assuming your unique ID is `unique-example`

This is the expected directory structure:

```
my-lambda-project/
├─ unique-example/
|  ├─ index.js
|  ├─ optional-dependency.js
|  ├─ optional-dependency.json
|  ├─ test/
|  |  ├─ my-tests.spec.js
|  |  ├─ more-tests.spec.js
|  |  ├─ optional-dependency.js
|  |  ├─ optional-dependency.json
├─ package.json
```
