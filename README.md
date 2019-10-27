# HerokuApp

## Configuration

Important!! You need to have a heroku account and one app created.

1. Move the follow dependencies from devDependencies to dependencies in package.json

```

"@angular/cli": "~8.3.14",
"@angular/compiler-cli": "~8.2.11",
"typescript": "~3.5.3"

```

2. Add the next script in package.json

```

"postinstall": "ng build --aot -prod"

```

With this script, when heroku or you do `npm install` and it finishes, npm runs this script and generates the dist folder with your app compiled.

3. Add the engines attribute in package.json

```

"engines": {
    "node": "v10.12.0",
    "npm": "6.11.2"
  }

```

With this attribute, you config the version of npm and node in heroku

4. Create the server to run your app.

Create a file with name `server.js` and next content:

```

//Install express server
const express = require('express');
const path = require('path');

const app = express();

// Serve only the static files form the dist directory
app.use(express.static(__dirname + '/dist/<name-of-app>'));

app.get('/*', function(req,res) {

res.sendFile(path.join(__dirname+'/dist/<name-of-app>/index.html'));
});

// Start the app by listening on the default Heroku port
app.listen(process.env.PORT || 8080);

```

Install the follow dependencies:

```

npm install express path --save

```

And replace the `start` script with the follow value in `package.json`:

```

"start": "node server.js"

```

5.
