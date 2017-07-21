# reproduce-npm-install-issue

This repository illustrates a use case in which one copies and pastes a Node.js package directly into the node_modules directory.
Then the application is pushed to a Cloud Foundry instance where the buildpack executes `npm install`. To make the example simpler,
the steps just include `npm install`ing with 2 different versions of npm.

Steps to reproduce:
- Clone this repository

- With npm v4.2.0 (used with Node.js v7.10.1), execute `npm install`. Output:

```
npm WARN app@1.0.0 No description
npm WARN app@1.0.0 No repository field.
npm WARN app@1.0.0 No license field.
```

Some warnings are displayed, the install itself is successful

- With npm v5.0.0 (used with Node.js v8.0.0), execute `npm install`. Output:

```
npm ERR! code E404
npm ERR! 404 Not Found: secret-package@1.0.0
```

The install is not successful.

This incompatibility seems to come from [this commit](https://github.com/npm/npm/commit/b97ef3594406d14f317e083bae6871583e40a7c3)
