# Editor settings for DX

## Saving changes

```
{
  "files.autoSave": "onFocusChange",
}
```

## Integrating JEST

vscode-jest extension needs to be installed first then add this to user settings to make jest work in the IDE when using Create-React-App and running jest with the jsdom environment.

```
{
  "jest.pathToJest": "npm run test --"
}
```

# Debugger for Chrome

Add the following to launch.json to add configurations for the web app and unit tests.

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Chrome",
      "type": "chrome",
      "request": "launch",
      "url": "http://localhost:3000",
      "webRoot": "${workspaceRoot}/src",
      "sourceMapPathOverrides": {
        "webpack:///src/*": "${webRoot}/*"
      }
    },
    {
      "name": "Debug CRA Tests",
      "type": "node",
      "request": "launch",
      "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/react-scripts",
      "args": ["test", "--runInBand", "--no-cache", "--env=jsdom"],
      "cwd": "${workspaceRoot}",
      "protocol": "inspector",
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen"
    }
  ]
}
```

If CRA is ejected then you might need to change the config similar to the following:

```json
"runtimeExecutable": "node",
"args": [
  "${workspaceRoot}/scripts/test.js",
  "--runInBand",
  "--no-cache",
  "--env=jsdom"
],
```

Note: executable permissions might be required on test.js
