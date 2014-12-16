#A web client for Irssi

Glowing Bear for Irssi is a web frontend for the [Irssi](http://irssi.org) IRC client and strives to be a modern interface. It is a fork of Glowing Bear for WeeChat. It relies on Irssi/Teddy to do all the heavy lifting and then provides some nice features on top of that, like embedding images, videos, and other content. The best part, however, is that you can use it from any modern internet device -- whether it's a computer, tablet, or smart phone -- and all your stuff is there, whereever you are. You don't have to deal with the messy technical details, and all you need to have installed is a browser or our app.

##Getting Started


Glowing Bear for Irssi connects to the Irssi instance you're already running, and you need to be able to establish a connection to the Irssi host from your device. It makes use of the teddy-nu websocket-proxy plugin, and therefore you need to load this script. If you want to get started as quickly as possible, use this command in Irssi after unpacking the teddy-nu script in the ~/.irssi/scripts folder:

	/run teddy-nu

Now point your browser to the address indicated! If you're having trouble connecting, check that the host and port of your Irssi host are entered correctly, and that your server's firewall permits incoming connections on the proxy port.

You can run Glowing Bear for Irssi in many ways: use it like any other webpage, as an app in Firefox (choose "Install app" on the landing page) or Chrome ("Tools", then "Create application shortcuts"), or a full-screen Chrome app on Android ("Add to homescreen").

For Android devices, you may want to check out [Teddy-Client for Android](https://github.com/aeirola/teddy-client) instead; [APK](http://koti.kapsi.fi/~aeirola/random/teddy-client/)


##Screenshots

Running as Firefox application in a separate window, and as Android app:

![Glowing Bear for Irssi screenshot](http://anti.teamidiot.de/static/nei/irssitab.png)
![Glowing Bear for Irssi screenshot](http://anti.teamidiot.de/static/nei/irssimobuffer.png)

Are you good with design? We'd love your help!
![Glowing Bear screenshot with lots of Comic Sans MS](https://4z2.de/glowing-bear3.png)

##How it Works

What follows is a more technical explanation of how Glowing Bear for Irssi works, and you don't need to understand it to use it.

Glowing Bear uses Irssi directly as its backend through the teddy-nu plugin. This means that we can connect to Irssi directly from the browser using WebSockets. Therefore, the client does not need a special "backend service", and you only need to install the teddy-nu script. A connection is made from your browser to your Irssi, with no services in between. Thus, Glowing Bear for Irssi is written purely in client-side JavaScript with a bit of HTML and CSS.

##FAQ

- *Can I use Glowing Bear to access a machine or port not exposed to the internet by passing the connection through my server?* No, that's not what Glowing Bear does. You can use a websocket proxy module for your webserver to forward `/teddy` to your Irssi instance though. Here are some pointers you might find helpful for setting this up with [nginx](http://nginx.com/blog/websocket-nginx/) or [apache](https://httpd.apache.org/docs/2.4/mod/mod_proxy_wstunnel.html).
- *How does the encryption work?* TLS is used for securing the connection if you enable encryption. This is handled by your browser, and we have no influence on certificate handling, etc. You can find more detailed instructions on how to communicate securely in the "encryption instructions" tab on the Glowing Bear for Irssi start page.

##Development

###Setup
Getting started with the development of Glowing Bear is really simple, partly because we don't have a build process (pure client-side JS, remember). All you have to do is clone the repository, fire up a webserver to host the files, and start fiddling around. You can try out your changes by reloading the page.

Here's a simple example using the python simple web server:
```bash
git clone https://github.com/glowing-bear/glowing-bear
cd glowing-bear
# python 2.*
python -m SimpleHTTPServer
# or python 3.*
python -m http.server
```

Now you can point your browser to [http://localhost:8000](http://localhost:8000)!


###Running the tests
Glowing Bear uses Karma and Jasmine to run its unit tests. To run the tests locally, you will first need to install `npm` on your machine. Check out the wonderful [nvm](https://github.com/creationix/nvm) if you don't know it already, it's highly recommended.

Once this is done, you will need to retrieve the necessary packages for testing Glowing-Bear (first, you might want to use `npm link` on any packages you have already installed globally):

`$ npm install`

Finally, you can run the unit tests:

`$ npm test`

Or the end to end tests:
`$ npm run protractor`

**Note**: the end to end tests assume that a web server is hosting Glowing Bear on `localhost:8000` and that Irssi/Teddy is configured on port 9001.

##Contributing

Whether you are interested in contributing or simply want to talk about the project, talk to anti@conference.jabber.teamidiot.de/Nei! For contributions that equally apply to Glowing Bear for WeeChat, you may want to get into contact with [upstream directly](https://github.com/glowing-bear/glowing-bear#contributing)

If you're curious about the projects we're using, here's a list: [AngularJS](https://angularjs.org/), [Bootstrap](http://getbootstrap.com/), [Underscore](http://underscorejs.org/), [favico.js](http://lab.ejci.net/favico.js/), Emoji provided free by [Emoji One](http://emojione.com/), and [zlib.js](https://github.com/imaya/zlib.js). Technology-wise, [WebSockets](http://en.wikipedia.org/wiki/WebSocket) are the most important part, but we also use [local storage](https://developer.mozilla.org/en-US/docs/Web/Guide/API/DOM/Storage#localStorage), the [Notification Web API](https://developer.mozilla.org/en/docs/Web/API/notification), and last (but not least) [Apache Cordova](https://cordova.apache.org/) for our mobile app.
