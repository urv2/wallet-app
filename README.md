
Digital wallet for [Colu](https://colu.co) assets.

Based on [Copay](https://github.com/bitpay/copay) 1.8 and [Colu SDK](http://documentation.colu.co/)

## Multiple asset wallets

Unicoisa allows to host multiple wallets for different assets using the same app instance. Which wallet to use is determined by URI: e.g. ``http://localhost:3000/foo`` will open wallet for `foo` configuration (see Installation section on how to set this up).

## Installation

Clone the source:

```sh
git clone https://github.com/troggy/unicoisa.git
cd copay
```

Install [bower](http://bower.io/) and [grunt](http://gruntjs.com/getting-started) if you haven't already:

```sh
npm install -g bower
npm install -g grunt-cli
```

Configure where to get config from:
Set `CONFIG_URL_BASE` env variable to the base URL of the service that serves configs. If not set, `https://dashboard.colu.co/config/wallets` will be used. This value will be joined together with wallet name. E.g. for wallet `foo` it will request config from ``https://dashboard.colu.co/config/wallets/foo``.
[Config file example](https://github.com/troggy/unicoisa/blob/master/config.js)

Build Copay:

```sh
bower install
npm install
grunt
npm start
```

Unicoisa is now ready to serve wallets for you configs (e.g. `foo` wallet will be served from `http://localhost:3000/foo`). Root page will redirect to `https://www.colu.co/` - could be configured with `HOME_PAGE` env variable

> **Note:** Other browser extensions could have access to Copay internal data and compromise the user's private key when running Copay as a web page.  For optimal security, you should disable all third-party browser extensions when using Copay in this manner.

## Build Copay App Bundles

### Android

- Install Android SDK
- Run `make android`

### iOS

- Install Xcode 6.1 (or newer)
- Run `make ios-prod`

##### Notes for Xcode 7.0

###### ATS support

Before starting Copay from Xcode, add these lines to "Custom iOS Target Properties":

```
<key>NSAppTransportSecurity</key>
 <dict>
  <key>NSAllowsArbitraryLoads</key>
  <true/>
 </dict>
```

![Example](http://i.stack.imgur.com/nGw3j.png)


App Transport Security (ATS) enforces best practices in the secure connections between an app and its back end. [Read complete documentation](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html).

###### Invalid Bundle while submitting application

`iPad Multitasking support requires launch story board in bundle`

To fix this problem, add the following:

```
<key>UIRequiresFullScreen</key>
<string>YES</string>
```
###### Build settings, headers search path

Add this line to your Build Settings -> Header Search Paths -> Release

"$(OBJROOT)/UninstalledProducts/$(PLATFORM_NAME)/include"



### Windows Phone

- Install Visual Studio 2013 (or newer)
- Run `make wp8-prod`

### Desktop versions (Windows, OS X, Linux)

Copay uses NW.js (also know as node-webkit) for its desktop version. NW.js is an app runtime based on `Chromium` and `node.js`.

- Install NW.js on your system from [nwjs.io](http://nwjs.io/)
- Run `grunt desktop`

### Google Chrome App

- Run `npm run-script chrome`

On success, the Chrome extension will be located at: `browser-extensions/chrome/copay-chrome-extension`.  To install it go to `chrome://extensions/` in your browser and ensure you have the 'developer mode' option enabled in the settings.  Then click on "Load unpacked chrome extension" and choose the directory mentioned above.

### Firefox Add-on

The Copay Firefox Extension has been deprecated and is no longer supported.

## License

Copay is released under the MIT License.  Please refer to the [LICENSE](https://github.com/bitpay/copay/blob/master/LICENSE) file that accompanies this project for more information including complete terms and conditions.
