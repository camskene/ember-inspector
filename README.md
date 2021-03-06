Ember Inspector [![Build Status](https://secure.travis-ci.org/emberjs/ember-inspector.svg?branch=master)](https://travis-ci.org/emberjs/ember-inspector)
===============

Adds an Ember tab to Chrome or Firefox Developer Tools that allows you to inspect
Ember objects in your application.

Installation
------------

### Chrome

Install the extension from the [Chrome Web Store](https://chrome.google.com/webstore/detail/ember-inspector/bmdblncegkenkacieihfhpjfppoconhi).

OR:

- Clone the repository
- cd into the repo directory
- run `npm install && bower install`
- run `npm install -g ember-cli`
- run `npm build` to build the `dist` directory
- Visit chrome://extensions in chrome
- Make sure `Developer mode` is checked
- Click on 'Load unpacked extension...'
- Choose the `dist/chrome` folder in the cloned repo
- Close and re-open developer tools if it's already open

### Firefox

Install the [Firefox addon](https://addons.mozilla.org/en-US/firefox/addon/ember-inspector/).

OR:

- Clone the repository
- cd into the repo directory
- run `npm install && bower install`
- run `npm install -g ember-cli`
- run `npm run build:xpi` to build the `dist` directory, download Firefox Addon SDK and build Firefox Addon XPI to 'tmp/xpi/ember-inspector.xpi'
  or `npm run run-xpi` to run the Firefox Addon in a temporary profile (or use `FIREFOX_BIN` and `FIREFOX_PROFILE` to customize Firefox profile directory and Firefox binary used to run the extension)

### Opera

- Clone the repository
- cd into the repo directory
- run `npm install`
- run `npm install -g ember-cli`
- run `npm build` to build the `dist` directory
- Visit chrome://extensions in chrome
- Make sure `Developer mode` is checked
- Click on 'Load unpacked extension...'
- Choose the `dist/chrome` folder in the cloned repo
- Close and re-open developer tools if it's already open


### Bookmarklet (All Browsers)


```javascript
javascript: (function() { var s = document.createElement('script'); s.src = '//ember-extension.s3.amazonaws.com/dist_bookmarklet/load_inspector.js'; document.body.appendChild(s); }());
```

Internet explorer will open an iframe instead of a popup due to the lack of support for cross-origin messaging.

For development:

- run `npm run serve:bookmarklet`
- create a bookmark (make sure you unblock the popup when you run the bookmarklet):

```javascript
javascript: (function() { var s = document.createElement('script'); s.src = 'http://localhost:9191/bookmarklet/load_inspector.js'; document.body.appendChild(s); }());
```


Building and Testing:
--------------------

Run `npm install && npm install -g ember-cli && && npm install -g bower && bower install && npm install -g grunt-cli` to install the required modules.

- `npm build` to build the files in the `dist` directory
- `npm run watch` To watch the files and re-build in `dist` when anything changes (useful during development).
- `npm test` To run the tests in the terminal
- `npm run build:xpi` to download and build Firefox Addon XPI into `tmp/xpi/ember-inspector.xpi`
- `npm run run-xpi` to run the Firefox Addon XPI on a temporary new profile (or use `FIREFOX_BIN` and `FIREFOX_PROFILE` to customize Firefox profile directory and Firefox binary used to run the extension)
- `npm start` To start the test server at `localhost:4200/testing/tests`


Deploy new version:
-----------

- Update `package.json` to new version and run `grunt version`
- `npm run build:production`
- Publish `dist/chrome/ember-inspector.zip` to the Chrome web store
- Publish `tmp/xpi/ember-inspector.xpi` to the Mozilla Addons
- 'git checkout stable && git merge master' and push the `stable` branch (to update the bookmarklet)
- `npm publish ./`
- `git tag` the new version


### Window Messages

The Ember Inspector uses window messages, so if you are using window messages in your application code, make sure you [verify the sender](https://developer.mozilla.org/en-US/docs/Web/API/window.postMessage#Security_concerns) and add checks to your event listener so as not to conflict with the inspector's messages.
