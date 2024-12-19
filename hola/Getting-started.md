# Installation

```bash
npm install happy-dom
```


# Usage

A simple example of how you can use Happy DOM.

```javascript
import { Window } from 'happy-dom';

const window = new Window({
   url: 'https://localhost:8080',
   width: 1024,
   height: 768
});
const document = window.document;

document.body.innerHTML = '<div class="container"></div>';

const container = document.querySelector('.container');
const button = document.createElement('button');

container.appendChild(button);

// Outputs "<div class="container"><button></button></div>"
console.log(document.body.innerHTML);
```

# Teardown

When closing a Happy DOM window, you should call `window.happyDOM.cancelAsync()`, which will clear timers and abort ongoing requests.

If you rather wish to wait for all async tasks to complete, you can call `await window.happyDOM.whenAsyncComplete()`. Note that this may take a long time, so you may want to implement some kind of timeout logic.

Read more under [Asynchronous Tasks](https://github.com/capricorn86/happy-dom/wiki/Asynchronous-Tasks).

# Virtual Console

Happy DOM uses a virtual console by default for all outputs to "window.console". You can read more about it under [Virtual Console](https://github.com/capricorn86/happy-dom/wiki/Virtual-Console).