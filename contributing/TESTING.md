Testing
==

All development should be accompanied with a corresponding unit and (if
applicable) end-to-end test. Feature work will not be approved for merge without
coverage. Similarly, bug fixes will not be approved for merge without a
corresponding regression test.

We use the following suite of tools for tests:

* **Mocha** for unit testing server-side code.
* **Karma and Jasmine** for unit testing Angular code.
* **Protractor** for end-to-end browser tests.
* **Istanbul** for code coverage reports.

Coverage reports are generated and stored in the `coverage` directory. These
reports are generated in both `html` for developer visualization and `lcov` for
reporting purposes.

[TravisCI](https://travis-ci.com) is used for Continuous Integration and will
run the entire test suite. End-to-end browser tests are executed using the
Firefox browser. All tests must be passing in TravisCI before the feature is
approved for merge.
