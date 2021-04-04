# Getting Started

[Jest](https://jestjs.io/) is a delightful JavaScript Testing Framework with a focus on simplicity. It works with projects using: Babel, TypeScript, Node, React, Angular, Vue and more!

# Installation

To install jest on specific project directory

```bash
yarn add --dev jest
#or 
npm install --save-dev jest
```

To install jest on global

```bash
npm install jest
```

# Configuration

## Add new script on `package.json`

Add new block on script section to run the test:

```json
...
"scripts": {
	...
  "test": "jest",
	...
},
...
```

## Generate basic configuration file

On the command line, run the code below to create basic configuration

```bash
jest --init
```

# How To Use

## Structuring the directory

There are two ways to store the test files.

-   _Unit test & integration test in the same directory_. This approach comes from the understanding that the test should be classified into one specific directory like config, service, and router directory.
    
    The app directory will be like the snippet below.
    
    ```bash
    mainAppDir
    - test
    	- unitTestDir
    		- appUnit.test.js
    	- integrationTestDir
    		- appIntegration.test.js
    - config
    	- config.json
    - service
    	- app.service.js
    - router
    	- app.router.js
    - util
    	- app.util.js
    ```
    
-   _Unit test in the same directory with the code while integration test in another directory_. This approach arises from the point of easiness to find the unit test for a specific function since it is located in the same directory. While the integration test should be located in one directory since it reflects the app functionality.
    
    The app directory will be like the snippet below
    
    ```bash
    mainAppDir
    - test
    	- appIntegration.test.js
    - config
    	- config.json
    - service
    	- app.service.js
    	- app.service.test.js
    - router
    	- app.router.js
    	- app.router.test.js
    - util
    	- app.util.js
    	- app.util.test.js
    ```
    

## Creating test

Let's start with creating `test` or `__test__` directory on the project directory. This directory used to store the testing file / configuration.

```bash
mkdir test 
#or 
mkdir __test__
```

Inside the directory, let's create test file. The test file should have `.test` prefix. e.g. `app.service.test.js`

There are several method that need to be used in order to create test file.

### `describe`

Used to group several related test. This method is optional, we can write test directly without this method.

```jsx
describe('sampe group of test', () => {
	...
})
```

### `test` or `it`

test or it method is method which run a test. If the function to test returns promise. Jest will wait for the promise to resolve before letting the test complete.

```jsx

describe('sampe group of test', () => {
	test('sample function test', () => {
		....
	})
})
```

### `expect` or matchers

expect is the method that used to evaluate the test results meet certain condition. JEST has a several matcher that can be used. Find more [here](https://jestjs.io/docs/using-matchers).

```jsx

describe('sampe group of test', () => {
	test('sample function test', () => {
		expect(function.to.test(paramA, paramB)).toBe(expectedResult);
	})
})
```

Another evaluation method that can be used are:

-   `toBe`
-   `toEqual`
-   `not`
-   `toBeNull`
-   `toBeUndefined`
-   `toBeDefined`
-   `toBeTruthy`

More info about matcher available [here](https://jestjs.io/docs/expect)

### Example

Let's say we have simple calculation function below to test

```jsx
const countFunction = (a, b) => {
	return a + b
}

module.exports = countFunction
```

The test will be

```jsx
const countFunction = require("./countFunction")

describe("count function", () => {
	expect(countFunction(1,2)).toBe(3);
})
```

## [Test Setup](https://jestjs.io/docs/setup-teardown)

If there are several work that need to be done on many test, we can use `beforeAll` or `beforeEach` and `afterEach` or `afterAll`

### `beforeEach` and `afterEach`

This method used to run functions / setup that need to be run every time test is take a place. e.g initialize the database or prepare the test data

```jsx
beforeEach(() => {
	prepareTestData()
})

afterEach(() => {
	cleanTestData()
})

test(...)
```

### `beforeAll` and `afterAll`

This method used to run function / setup that need to be run once when test is take a place. e.g open database connection

```jsx
beforeAll(() => {
	openDatabase()
})

afterAll(() => {
	closeDatabase()
})

test(...)
```

The `before` and `after` block can be used inside group (`describe` block) or outside the block. When it is used inside the group, the `before` and `after` block will only apply to the group. Read more about it on [here](https://jestjs.io/docs/setup-teardown#scoping).

## [Test Asynchronous Code](https://jestjs.io/docs/asynchronous)

There are several way to test asynchronous function depends on the function, below are some example of it.

### [Callback](https://jestjs.io/docs/asynchronous#callbacks)

```jsx
test('the data is peanut butter', done => {
  function callback(data) {
    try {
      expect(data).toBe('peanut butter');
      done();
    } catch (error) {
      done(error);
    }
  }

  fetchData(callback);
});
```

### [Promises](https://jestjs.io/docs/asynchronous#promises)

```jsx
test('the data is peanut butter', () => {
  return fetchData().then(data => {
    expect(data).toBe('peanut butter');
  });
});
```

### [.resolves / .rejects](https://jestjs.io/docs/asynchronous#resolves--rejects)

```jsx
test('the data is peanut butter', () => {
  return expect(fetchData()).resolves.toBe('peanut butter');
});
```

### [Async/Await](https://jestjs.io/docs/asynchronous#asyncawait)

```jsx
test('the data is peanut butter', async () => {
  await expect(fetchData()).resolves.toBe('peanut butter');
});

test('the fetch fails with an error', async () => {
  await expect(fetchData()).rejects.toThrow('error');
});
```

# Setup Code Coverage

[Code coverage](https://www.atlassian.com/continuous-delivery/software-testing/code-coverage) is a metric that can help to understand how much the source code is tested. The metrics that used to calculate the coverage reports include:

-   **Function coverage**: how many of the functions defined have been called.
-   **Statement coverage**: how many of the statements in the program have been executed.
-   **Branches coverage**: how many of the branches of the control structures (if statements for instance) have been executed.
-   **Condition coverage**: how many of the boolean sub-expressions have been tested for a true and a false value.
-   **Line coverage**: how many of lines of source code have been tested.

### Enable Code Coverage

Edit the `jest.config.js` as below:

```jsx
module.exports = {
  ...
  // Indicates whether the coverage information should be collected while executing the test
  collectCoverage: true,

  // An array of glob patterns indicating a set of files for which coverage information should be collected
  // collectCoverageFrom: undefined,

  // The directory where Jest should output its coverage files
  coverageDirectory: 'coverage',

  // An array of regexp pattern strings used to skip coverage collection
  // coveragePathIgnorePatterns: [
  //   "/node_modules/"
  // ],

  // Indicates which provider should be used to instrument code for coverage
  coverageProvider: 'v8',

  // A list of reporter names that Jest uses when writing coverage reports
  coverageReporters: ['lcov', 'text-summary', 'cobertura'],

  // An object that configures minimum threshold enforcement for coverage results
  coverageThreshold: {
    global: {
      branches: 0,
      functions: 0,
      lines: 0,
      statements: 0,
    },
  },
	...
};
```

The coverage report will be available under `coverage` directory. The example report:

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dbe2933f-fa7d-49c1-9d6a-02ef266884e7/2021-03-17_13-42.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dbe2933f-fa7d-49c1-9d6a-02ef266884e7/2021-03-17_13-42.png)

# Gitlab automation

---

Follow the step below to setup gitlab automation

## Install and configure [jest-junit](https://www.npmjs.com/package/jest-junit)

Since gitlab support xml as the coverage result, we can use [jest-junit](https://www.npmjs.com/package/jest-junit) to generate the compatible xml report

```bash
npm install --save-dev jest-junit
```

Once installed, let's update the `jest.config.js` to add jest-junit as reporters

```jsx
module.exports = {
	...
  // Use this configuration option to add custom reporters to Jest
  reporters: ['default', ['jest-junit', {outputDirectory: './artifacts'}]],
	...
};
```

## Update `gitlab-ci.yml`

Add new block to enable the test automation

```yaml
stages:
  - test

javascript:
  stage: test
  before_script:
    - npm install
# adjust the path as needed
    - cd backend && npm install 
  script:
    - npm run test
  artifacts:
    when: always
# adjust the path as needed
    paths:
        - ./backend/junit.xml
        - ./backend/coverage/cobertura-coverage.xml
    reports:
      junit:
        - ./backend/junit.xml
      cobertura: ./backend/coverage/cobertura-coverage.xml
```

Action on the block above are includes:

-   install needed packages
-   run the test
-   upload the test and coverage result to gitlab.

# References

[](https://www.albertgao.xyz/2017/05/24/how-to-test-expressjs-with-jest-and-supertest/)[https://www.albertgao.xyz/2017/05/24/how-to-test-expressjs-with-jest-and-supertest/](https://www.albertgao.xyz/2017/05/24/how-to-test-expressjs-with-jest-and-supertest/)

[](https://jestjs.io/docs/en/getting-started)[https://jestjs.io/docs/en/getting-started](https://jestjs.io/docs/en/getting-started)

[](https://jestjs.io/docs/en/testing-frameworks)[https://jestjs.io/docs/en/testing-frameworks](https://jestjs.io/docs/en/testing-frameworks)

[](https://jestjs.io/en/)[https://jestjs.io/en/](https://jestjs.io/en/)

[](https://medium.com/swlh/react-testing-using-jest-along-with-code-coverage-report-7454b5ba0236)[https://medium.com/swlh/react-testing-using-jest-along-with-code-coverage-report-7454b5ba0236](https://medium.com/swlh/react-testing-using-jest-along-with-code-coverage-report-7454b5ba0236)

[](https://docs.gitlab.com/ee/ci/unit_test_reports.html)[https://docs.gitlab.com/ee/ci/unit\_test\_reports.html](https://docs.gitlab.com/ee/ci/unit_test_reports.html)

[](https://medium.com/@mutebg/using-gitlab-to-build-test-and-deploy-modern-front-end-applications-bc940501a1f6)[https://medium.com/@mutebg/using-gitlab-to-build-test-and-deploy-modern-front-end-applications-bc940501a1f6](https://medium.com/@mutebg/using-gitlab-to-build-test-and-deploy-modern-front-end-applications-bc940501a1f6)

[](https://gist.github.com/superjose/709989dd58aa90bfeda75767668482b2)[https://gist.github.com/superjose/709989dd58aa90bfeda75767668482b2](https://gist.github.com/superjose/709989dd58aa90bfeda75767668482b2)

[](https://medium.com/walkin/beginners-guide-to-testing-with-jest-31f1826baf4a)[https://medium.com/walkin/beginners-guide-to-testing-with-jest-31f1826baf4a](https://medium.com/walkin/beginners-guide-to-testing-with-jest-31f1826baf4a)

#jest #testing-framework