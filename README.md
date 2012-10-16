# Trello base app

Trello base app is an express squeleton to create apps on top of trello.

It provides:

* trello login (oauth1 authentication dance)
* trello deauthorization
* session store in redis
* API access to trello via Backbone models
* metrics on all actions

## Install

    npm install trello_baseapp

## Usage

### Get the express app

To get the basic express app, you have to provide a config object:

    var config = {
      "trello": {
        "token": {
        "name": "Your app name",
        "expiration": "never",
        "scope": "read,write"
      },
      "key": "",
      "secret": ""
      }
    };

    var app = require('trello_baseapp/lib/app')(config);

### Login user

To log a user, redirect it to `/login`.

## Deauthorize

To deauthorize the application and logout the user:

    DELETE /deauthorize

### Using models

If a user if logged-in, you can use some backbone models via the request parameter.

```javascript
app.get('/me', function(req, res) {
    var boards = req.trello.Boards();
    boards.fetch({
        success: function() {
            res.send('ok');
        },
        error: function() {
            res.send('error', 500);
        }
    });
});
```

## License

(c) 2012 François de Metz

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.
