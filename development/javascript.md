# Javascript

- [Javascript](#javascript)
  - [Resources](#resources)
  - [Miscellaneous Tips](#miscellaneous-tips)
    - [Dates in Javascript](#dates-in-javascript)
    - [Every prototype](#every-prototype)
    - [Firebug vs Firefox Development Tools](#firebug-vs-firefox-development-tools)
    - [Google Map API](#google-map-api)
  - [Node & NPM](#node--npm)
    - [Node JS](#node-js)
    - [Issues with Node permissions](#issues-with-node-permissions)
    - [What happens if you do standard install of node](#what-happens-if-you-do-standard-install-of-node)
      - [uninstalling this mess](#uninstalling-this-mess)
    - [Install Node using NVM (PREFERRED WAY APPARENTLY)](#install-node-using-nvm-preferred-way-apparently)
      - [Running node (or other node libraries) V.IMPORTANT](#running-node-or-other-node-libraries-vimportant)
      - [Updating npm](#updating-npm)
    - [Installing Yarn](#installing-yarn)
    - [Markdown Linter & Commandline version](#markdown-linter--commandline-version)
  - [JQuery](#jquery)
    - [Selecting Previous Siblings](#selecting-previous-siblings)
    - [Misusing return false in functions](#misusing-return-false-in-functions)
    - [Selecting text](#selecting-text)
    - [Handy way to make text input numeric](#handy-way-to-make-text-input-numeric)
  - [Mobile Development](#mobile-development)
  - [CSS Selectors](#css-selectors)
    - [Drop Down Menu Example](#drop-down-menu-example)
    - [JS Chart Libraries](#js-chart-libraries)
  - [Bootstrap](#bootstrap)
  - [Backbone JS](#backbone-js)
  - [JSON](#json)
    - [JSON Object Example](#json-object-example)
    - [JSON objects in Postman](#json-objects-in-postman)
    - [Tutorials n Stuff](#tutorials-n-stuff)

## Resources

- Mozilla Java Script Guide -
    <https://developer.mozilla.org/bm/docs/Web/JavaScript>
  - <https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps>
- 2018 Front-end Handbook:
    <https://frontendmasters.com/books/front-end-handbook/2018/>
- Form Data and HTTP Client
  - <https://developer.mozilla.org/en-US/docs/Web/API/FormData>
        provides a way to easily construct a set of key/value pairs representing form fields and their values
  - <https://github.com/axios/axios> Promise based HTTP client for the browser and node.js

## Miscellaneous Tips

### Dates in Javascript

getDate() method returns the current day of the month and NOT a date
object 8-)

```javascript
 date.getDate();
```

### Every prototype

Every can be used to test every element in the array and return one
boolean value based on the result of the test.
<https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every>

```javascript
 var result = [1, 30, 40, 29, 10, 13].every(currentValue => currentValue <= 40);
```

### Firebug vs Firefox Development Tools

<https://developer.mozilla.org/en-US/docs/Tools/Migrating_from_Firebug>

### Google Map API

Setting map to fit bounds of markers

```javascript
markers =[marker_obj_1, marker_obj_2, marker_obj_3];
new_boundary =new google.maps.LatLngBounds();
for(index in markers){
 position = markers[index].position; new_boundary.extend(position);
}
map.fitBounds(new_boundary);
```

solving issue of multiple calls to fit bounds
<http://stackoverflow.com/questions/11336405/google-maps-api-v3-fitbounds-after-multiple-geocoder-requests?rq=1>

## Node & NPM

### Node JS

- InfoQ article:
    <http://www.infoq.com/resource/articles/nodejs-in-action/en/resources/NodejsinActionCH03.pdf>

### Issues with Node permissions

By default node/npm can end up needing to be installed by sudo (default
paths are in /usr/local/lib\....). This then causes issues because you
can\'t run anything without using sudo\....

- Original post on working around permissions issues -
    <https://www.competa.com/blog/how-to-run-npm-without-sudo/>
- Newer post about using NVM -
    <https://www.competa.com/blog/use-nvm-for-fun-and-profit-and-to-run-npm-without-sudo/>

### What happens if you do standard install of node

It seems the standard sudo apt get install way of installing node + npm is WRONG and will give you permissions issues when you try to 
install other stuff (global packages) e.g. yarn

```bash
14:45 $ npm ls -gp --depth=0 | awk -F/ '/node_modules/ && !/\/npm$/ {print $NF}' | xargs npm -g rm
npm ERR! code EACCES
npm ERR! syscall rename
npm ERR! path /usr/lib/node_modules/corepack
npm ERR! dest /usr/lib/node_modules/.corepack-Ly9MGgoL
npm ERR! errno -13
npm ERR! Error: EACCES: permission denied, rename '/usr/lib/node_modules/corepack' -> '/usr/lib/node_modules/.corepack-Ly9MGgoL'
npm ERR!  [Error: EACCES: permission denied, rename '/usr/lib/node_modules/corepack' -> '/usr/lib/node_modules/.corepack-Ly9MGgoL'] {
npm ERR!   errno: -13,
npm ERR!   code: 'EACCES',
npm ERR!   syscall: 'rename',
npm ERR!   path: '/usr/lib/node_modules/corepack',
npm ERR!   dest: '/usr/lib/node_modules/.corepack-Ly9MGgoL'
npm ERR! }
npm ERR! 
npm ERR! The operation was rejected by your operating system.
npm ERR! It is likely you do not have the permissions to access this file as the current user
npm ERR! 
npm ERR! If you believe this might be a permissions issue, please double-check the
npm ERR! permissions of the file and its containing directories, or try running
npm ERR! the command again as root/Administrator.

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/dcostello/.npm/_logs/2022-04-15T12_46_14_181Z-debug-0.log
```

#### uninstalling this mess

- based on this stackoverflow - <https://stackoverflow.com/a/33947181/864024>

```bash
sudo apt-get remove nodejs

# When I ran this command it said nothing was installed so maybe the first command was enough - 
# Error was: "Package 'npm' is not installed, so not removed"
sudo apt-get remove npm 

# Then go to /etc/apt/sources.list.d and remove any node list if you have. 
sudo rm /etc/apt/sources.list.d/nodesource.list

# Then this
sudo apt-get update

# Finally get rid of .npm from home dir
rm -rf ~/.npm/

# Sanity check - shouldn't find anything
which node
which nodejs
which npm
```

### Install Node using NVM (PREFERRED WAY APPARENTLY)

- <https://github.com/nvm-sh/nvm>
  - The page proposes to install using this line 
    - wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
    - It creates/copies content to ~/.nvm
    - It updates your profile/bash file (in my case .bashrc) with some env info

```bash
# This was added to ~/.bashrc - I also added the "no-use" but not sure if it's taken into account correctly :)
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

- Then can launch a new terminal to check if nvm was installed correctly

```bash
# Should output nvm if installed correctly, see github page for readme and troubleshooting
$ command -v nvm
nvm

# NB - which nvm doesn't find anything since it's a script
```

- After that to install node & npm

```bash
# Version string or blank for latest version
$ nvm install 16.14.2

# Check versions
$ node --version
v16.14.2
$ npm --version
8.5.0

# list versions local or remote
nvm ls
nvm ls-remote
```

#### Running node (or other node libraries) V.IMPORTANT

After doing the install of nvm, to use node, just do this:

```bash
nvm use node
```

#### Updating npm

- Can update npm through itself :), node should be handled by the nvm though

```bash
npm install -g npm
```

### Installing Yarn

- Classic version

After setting up node as per instructions above, then run

```bash
npm install --global yarn
```

- Overview + Docs for yarn - <https://classic.yarnpkg.com/en/docs/getting-started>
- Apparently there is a newer non-backward compatible version also :)

### Markdown Linter & Commandline version

There\'s a markdown linter add on for VS Code which is REALLY nice and
there\'s also a cmd-line version that can be used to generate
reports\...

- <https://github.com/DavidAnson/markdownlint>
- <https://github.com/igorshubovych/markdownlint-cli>

Javascript Frameworks

- Underscore, Backbone, Marionette - Replacement for JQuery for MVC
    structure.
- JQuery - for everything!
- NodeJS
- AngularJS
- EmberJS

## JQuery

### Selecting Previous Siblings

<http://api.jquery.com/next-siblings-selector/> example of selecting
previous siblings.

Example here selects the first span sibling of this element.

```javascript
        $('span[price] input[type=text]').change(function(){
            $('~ span:first',this).text(
                $(this).val() *
                        $(this).parents("span[price]:first").attr('price')
                );
        });
```

### Misusing return false in functions

<http://fuelyourcoding.com/jquery-events-stop-misusing-return-false/>

### Selecting text

```javascript
 .val() // for input boxes and form fields
 .text() // get or set plain text values
 .html() // get or set html
```

Can append to jQuery selection objects:

```javascript
  $('#results').append(result);
```

### Handy way to make text input numeric

Allows you to use it in calculations. NB snippet below has no error
checking whatsoever

```javascript
  var heightText = $('#heightText').val()*1;
```

## Mobile Development

jQuery Mobile - v good with PhoneGap

<http://mobile.tutsplus.com/tutorials/mobile-web-apps/use-jquery-mobile-to-build-a-native-android-news-reader-app-part-3/>

## CSS Selectors

Example of selectors in JQuery.
<http://www.pamaya.com/jquery-selectors-and-attribute-selectors-reference-and-examples/>

### Drop Down Menu Example

Stay tuned for github version of JDiv from me\... Also another version
of the same - <http://jsfiddle.net/roXon/77CXH/>

### JS Chart Libraries

- <http://www.jqwidgets.com/jquery-widgets-demo/demos/jqxchart/>
- <http://www.computerworld.com/s/article/9237337/Six_useful_JavaScript_libraries_for_dealing_with_data>
- <http://javascripted.me/top-5-free-javascript-chart-libraries.html>

## Bootstrap

Bootstrap - A Framework that started with a couple of developers at
Twitter. Provides css, widgets, html and JS <http://getbootstrap.com>

## Backbone JS

Backbone JS is an MVC framework for rich web apps

- Tutorial - <http://arturadib.com/hello-backbonejs/>
- Homepage of the Framework -
    <http://documentcloud.github.io/backbone/>

## JSON

### JSON Object Example

```javascript
var myJSONObject = {"bindings": [
        {"ircEvent": "PRIVMSG", "method": "newURI", "regex": "^http://.*"},
        {"ircEvent": "PRIVMSG", "method": "deleteURI", "regex": "^delete.*"},
        {"ircEvent": "PRIVMSG", "method": "randomURI", "regex": "^random.*"}
    ]
};
```

### JSON objects in Postman

```javascript
pm.test("Successful HTTP 200", function () {
  pm.response.to.have.status(200);
});

pm.test("has results", function () {
  const responseJson = xml2Json(pm.response.text());
  const response = responseJson?.SomeResponse?.Response;
  
  pm.expect(response).to.be.not.undefined;
  
  // Optional selector for nested objects - if any null, returns undefined without error
  pm.environment.set("1N_shopping_response_id", response?.BodyReply?.Item[0]);
});

### Tutorials n Stuff

- Good series of videos on Javascript: <http://yuiblog.com/crockford/>
- (JS Ninja) Possibly good book on JS in general and with focus on JS
    libraries : <http://www.manning.com/resig/>
- <https://github.com/DavidAnson/markdownlint>
- <https://github.com/igorshubovych/markdownlint-cli>
