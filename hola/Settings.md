# URL

The URL can be sent as a property to the constructor. The URL defaults to "about:blank".

The URL has to be set in order for relative URL:s to work in the Happy DOM environment.

```javascript
const window = new Window({
   url: 'https://localhost:8080'
});
```

## setURL()

Sets the property `Window.location.href`.

```javascript
window.happyDOM.setURL('https://localhost:3000');
```

# Window Size

The window size can be sent as properties to the constructor. The window size defaults to the width "1024" and height "768".

```javascript
const window = new Window({
   width: 1920,
   height: 1080
});
```

## setWindowSize()

Sets the properties `Window.innerWidth` and `Window.innerHeight`. Dispatches a "resize" event.

```javascript
window.happyDOM.setWindowSize({ width: 1920, height: 1080 });
```
# Console
Happy DOM uses a [Virtual Console](https://github.com/capricorn86/happy-dom/wiki/Virtual-Console) by default on the `Window.console` property. It is possible to send in another console to the constructor.

```javascript
const window = new Window({
   console: global.console
});
```

# Settings

Settings can be sent to the constructor.

```javascript
const window = new Window({
   settings: {
       disableJavaScriptFileLoading: true,
       disableJavaScriptEvaluation: true,
       disableCSSFileLoading: true,
       disableIframePageLoading: true,
       disableComputedStyleRendering: true,
       disableErrorCapturing: true,
       enableFileSystemHttpRequests: true,
       navigator: {
          userAgent: 'Mozilla/5.0 (Win32) AppleWebKit/537.36 (KHTML, like Gecko) MyCustomBrowser/1.0'
       },
       device: {
          mediaType: 'print',
          prefersColorScheme: 'dark
       }
    }
});
```

## Available Settings

| Name | Description | Default Value |
|------|-------------|---------------|
| disableJavaScriptFileLoading | Set it to "true" to disable JavaScript file loading. | false |
| disableJavaScriptEvaluation | Set it to "true" to completely disable JavaScript evaluation. | false |
| disableCSSFileLoading | Set it to "true" to disable CSS file loading in HTMLLinkElement. | false |
| disableIframePageLoading | Set it to "true" to disable page loading in HTMLIFrameElement. | false |
| disableComputedStyleRendering | Set it to "true" to disable the simulation of rendering when calculating computed style. The rendering process will convert values such as "rem", "em", "cm" etc. to pixels. However, it is currently very limited and will therefore not always give the same result as the browser. | false |
| disableErrorCapturing | Happy DOM will by default try to catch errors in functionality such as scripts, timers and event listeners. This setting makes it possible to disable this functionality and handle errors yourself (e.g. by using @happy-dom/uncaught-exception-observer). To run code without try/catch can improve performance significantly. | false |
| enableFileSystemHttpRequests | Set it to "true" to enable file system HTTP requests using XMLHttpRequest. | false |
| navigator.userAgent | The browser user agent string. It is used by Window.navigator, Window.fetch() and XMLHttpRequest. | "Mozilla/5.0 (X11; {process.platform} {process.arch}) AppleWebKit/537.36 (KHTML, like Gecko) HappyDOM/{packageVersion}" |
| device.mediaType | Used by media queries. Acceptable values are "screen" or "print". | "screen" |
| device.prefersColorScheme | Used by media queries. Acceptable values are "light" or "dark". | "light" |

## Changing Settings

Settings are available in the `Window.happyDOM.settings`object and can be changed runtime.

```javascript
const window = new Window();

window.happyDOM.settings.disableJavaScriptFileLoading = true;
window.happyDOM.settings.disableJavaScriptEvaluation = true;
window.happyDOM.settings.disableCSSFileLoading = true;
window.happyDOM.settings.disableIframePageLoading = true;
window.happyDOM.settings.disableComputedStyleRendering = true;
window.happyDOM.settings.disableErrorCapturing = true;
window.happyDOM.settings.enableFileSystemHttpRequests = true;
window.happyDOM.settings.navigator.userAgent = 'Mozilla/5.0 (Win32) AppleWebKit/537.36 (KHTML, like Gecko) MyCustomBrowser/1.0';
window.happyDOM.settings.device.mediaType = 'print';
window.happyDOM.settings.device.prefersColorScheme = 'dark';
```