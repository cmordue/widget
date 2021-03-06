[![Build Status](https://auth0-tc-hub.herokuapp.com/bt23/status.png)](https://auth0-tc-hub.herokuapp.com/bt23)
[![NPM version](https://badge.fury.io/js/auth0-widget.js.png)](http://badge.fury.io/js/auth0-widget.js)

[![Auth0](http://blog.auth0.com.s3.amazonaws.com/logo-290x200-letters.png)](http://auth0.com)

[Auth0](http://auth0.com) is an authentication broker that supports social identity providers as well as enterprise identity providers such as Active Directory, LDAP, Office365, Google Apps, Salesforce.

The Auth0 Login Widget makes it easy to integrate SSO in your app. You won't have to worry about:
* Having a professional looking login dialog that displays well on any resolution and device.
* Finding the right icons for popular social providers.
* Remembering what was the identity provider the user chose the last time.
* Solving the home realm discovery challenge with enterprise users (i.e.: asking the enterprise user the email, and redirecting to the right enterprise identity provider).
* Implementing a standard sign in protocol (OpenID Connect / OAuth2 Login)

## Usage

Take `auth0-widget.js` or `auth0-widget.min.js` from the `build` directory and import it to your page.

### Initialize:

Construct a new instance of the Auth0 Widget as follows:

~~~html
<script src="auth0-widget.min.js"></script>
<script type="text/javascript">
  var widget = new Auth0Widget({
    domain:       'mine.auth0.com',
    clientID:     'dsa7d77dsa7d7',
    callbackURL:  'http://my-app.com/callback'
  });

  // ...
</script>
~~~

### Show Widget:

To invoke the widget, use the `show` method:

~~~javascript
widget.signin();
// or
widget.signin(options, callback);
~~~

#### Options

* __connections__: Array of enabled connections that will be used for the widget. _Default: all enabled connections_.
* __container__: The id of the DIV where the widget will be contained.
* __icon__: Icon url. _Recommended: 32x32_.
* __showIcon__: Show/Hide widget icon. _Default: false_.

~~~javascript
widget.signin({
  connections: ['facebook', 'google-oauth2', 'twitter', 'Username-Password-Authentication', 'fabrikam.com'],
  container: 'root',
  icon: 'https://s3.amazonaws.com/assets.fabrikam.com/w2/img/logo-32.png',
  showIcon: true
}, funcion () {
  // The Auth0 Widget is now loaded.
});
~~~

## `signup` and `reset`

It is also possible to start the widget in the __Sign Up mode__ or __Reset Password__ mode as follows:

~~~javascript
widget.signup(/* [same as the .signin method] */)

// or

widget.reset(/* [same as the .signin method] */)
~~~

## Single Page Applications

You can handle the authorization process client-side as follows:

~~~javascript
<script type="text/javascript">
  var widget = new Auth0Widget({
    domain:       'mine.auth0.com',
    clientID:     'dsa7d77dsa7d7',
    callbackURL:  'http://my-app.com/',
    callbackOnLocationHash: true
  });

  widget.parseHash(window.location.hash, function (profile, id_token, access_token, state) {
    alert('hello ' + profile.name);
    //use id_token to call your rest api
  });
</script>
~~~

## i18n

__Note 1:__ most of the translations are machine generated, please help us to move this forward.

Version `1.2.0` we added support for internationalization:

![](http://s3.amazonaws.com/blog.auth0.com/login_langs.gif)

You can call instantiate the widget with the `dict` option:

~~~javascript
  var widget = new Auth0Widget({
    domain:       'mine.auth0.com',
    clientID:     'dsa7d77dsa7d7',
    callbackURL:  'http://my-app.com/',
    dict:         'es'
  });
~~~

where dict can be a string matching the name of the file in the `i18n` folder or it could be an object literal as follows:

~~~javascript
  var widget = new Auth0Widget({
    domain:       'mine.auth0.com',
    clientID:     'dsa7d77dsa7d7',
    callbackURL:  'http://my-app.com/',
    dict:         {
      "loadingTitle": "loading...",
      "close": "close",
      "signin": {
      ..//same as in i18n json files
    }
  });
~~~

## Customize the look and feel

Apply your own style to the elements.

All classes and ids are prefixed with `a0-` to avoid conflicts with your own stylesheets.

Send us an screenshot! We would love to see what you can do.

## Example

The example directory has a ready-to-go app. In order to run it you need [node](http://nodejs.org/) installed and grunt (npm i grunt -g), then execute `grunt example` from the root of this project.

## Develop

Run `grunt dev` and point your browser to `http://localhost:9999/test_harness.html` to run the test suite.

## Browser Compatibility

We are using [BrowserStack](http://browserstack.com) to run the test suite on multiple browsers on every push.

## License

The MIT License (MIT)

Copyright (c) 2013 AUTH10 LLC

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
