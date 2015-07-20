# firebase-react-native

## This library is now deprecated!

As of v2.2.7, firebase now has great support for react-native. I highly recommend using the official library instead: `npm i firebase --save`

#### Instructions

Currently, the firebase client api doesn't support react native.  There are few reasons:

- JSC doesn't include WebSockets, so it has to be polyfilled
- firebase.js uses DOM stuff like document.createElement to create iframes. This isn't available in JSC either
- firebase.js expects to be run inside of a browser or node, and neither are quite the same as running javascript with react-native

So, I essentially hacked the latest version of firebase-debug.js to death, and now it works with react native when used in conjunction with [Harrison Harnish's excellent websocket polyfill](https://github.com/hharnisc/react-native).  
#### Disclaimer
As mentioned above, this is super hacky and barely tested.  Don't try to use this in production.  Eventually firebase and react-native will play nice together and this repo will become obsolete.  But for now, you're able to mash the two together and have some fun.


#### Usage

`npm install --save firebase-react-native`

Then start using it in your code:
`var Firebase    = require('firebase-react-native');`

You also need to import the websocket polyfill into your react-native project.  Below are instructions I use, but there may be easier paths with less steps:

- clone the fork of react-native with websocket polyfill https://github.com/hharnisc/react-native
- copy the [WebSocket](https://github.com/hharnisc/react-native/tree/master/Libraries/WebSocket) folder into your react-native/Libraries folder.  This is probably inside of Node_Modules
- drag and drop the https://github.com/hharnisc/react-native/tree/master/Libraries/WebSocket/RCTWebSocket.xcodeproj into the `Libraries` folder in your XCode project
- Select your project in Xcode and on the properties page select the General tab.  In "Linked Frameworks and Libraries" click the plus button and add `libWebSocket.a`
- Go into your favorite text editor again, and replace `node_modules/react-native/Libraries/JavaScriptAppEngine/Initialization/InitializeJavaScriptAppEngine.js` with the [one that bootstraps the WebSocket](https://github.com/hharnisc/react-native/blob/master/Libraries/JavaScriptAppEngine/Initialization/InitializeJavaScriptAppEngine.js)
