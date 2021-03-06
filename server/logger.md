## Logger

Anvil Connect uses [bunyan](https://github.com/trentm/node-bunyan) for logging.

### JSON Example

The default `stdout` and `file` streams can be enabled or disabled by editing your JSON configuration file. The default log level is INFO, 
but it can be specified here too.

```json
{
  // ...
  "logger": {
    "stdout": true,
    "file": true,
    "level": "debug"
  }
}
```

### JavaScript Example

You can also create more sophisticated logging schemes with fine-grained log levels by creating a module called `logger.js` in the same directory of your project as `server.js`.

```javascript
module.exports = {
  name: 'anvilconnect',
  streams: [
    {
      level: 'info',
      stream: process.stdout            // log INFO and above to stdout
    },
    {
      level: 'error',
      path: '/var/tmp/myapp-error.log'  // log ERROR and above to a file
    }
  ]
}
```

## Configuration Options

```json
  level: fatal|error|warn|info|debug|trace
```

See [Bunyan's log level options](https://github.com/trentm/node-bunyan#levels) for more information on the meaning behind these configuration options.

### Parsing Log Output

__Stdout__

```
  # Run Anvil locally and pretty-print all logs.
  node server.js | node_modules/.bin/bunyan
  
  # Run Anvil locally and show 'warn' logs or above.
  node server.js | node_modules/.bin/bunyan -l warn
  
  # Run Anvil locally and ONLY show debug logs.
  node server.js | node_modules/.bin/bunyan -c 'this.level == 20'
```

Also see [Bunyan CLI](https://github.com/trentm/node-bunyan#cli-usage).
