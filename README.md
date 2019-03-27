# pingmydyno

> Keep Heroku dynos awake forever ☕️

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Why?

Heroku (free) dynos are great for hosting apps and showing them off to
your boss/friends or potential employer. The downside is, your app
will fall asleep 😴 if it doesn't receive any web traffic within a 30-minute
window. `pingmydyno` aims to solve this by making sure your dyno never fall
asleep.

## Features

- Forever dyno pings
- Automatically retry ping on failure

## Installation

```bash
npm install pingmydyno

# or using yarn

yarn install pingmydyno
```

## Usage

With Express.js (ES6 module)

```javascript
...
import express from 'express';
import pingmydyno from 'pingmydyno';

const app = express();

...

app.listen(PORT, () => {
    console.log('server running');
    pingmydyno('https://myapp.herokuapp.com');
});

```

With Hapi.js (commonJS)

```javascript
const Hapi = require('hapi');
const pingmydyno = require('pingmydyno');

const server = Hapi.server({ port, host });

async () => {
  await server.start();
  console.log('server running');
  pingmydyno('https://myapp.herokuapp.com');
};
```

## APIs

**pingmydyno(url, [Config])**

### url

Type: `string`

Required: `yes`

### Config

Type: `Object`

Required: `no`

| object       | value                 | default    | description                                          |
| ------------ | --------------------- | ---------- | ---------------------------------------------------- |
| pingInterval | number (milliseconds) | 1200000    | interval between the next ping                       |
| maxRetry     | number                | 2          | retry times when ping fail                           |
| onSuccess    | function              | ( ) => null | callback function called when a ping is successful   |
| onFailure    | function              | ( ) => null | callback function called when `maxRetry` ping failed |

## Contributing

1. Fork the repo
2. Create your feature branch (`git checkout -b my-awesome-feature`)
3. Add your awesome feature
4. Commit your changes (`git commit -am 'Awesome feature added'`)
5. Push to the branch (`git push origin my-awesome-feature`)
6. Submit a Pull Request

## License

This project is license under
[MIT](https://github.com/codeshifu/pingmydyno/blob/master/LICENSE)
