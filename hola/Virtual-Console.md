Happy DOM uses a virtual console by default on the `Window.console` property.

The virtual console outputs log entries to a Virtual Console Printer. The log entries are buffered until read.


## Reading the Log

### As a String
```javascript
import { Window, VirtualConsoleLogLevelEnum } from 'happy-dom';

const window = new Window();

window.console.log('Test', { test: true });

const log = window.happyDOM.virtualConsolePrinter.readAsString(VirtualConsoleLogLevelEnum.log);

// Will output 'Test {"test": true}' to the NodeJS console
global.console.log(log);
```

### As Log Entries

Each entry contains data about its "type", "level", "message" and "group". It is therefore possible to filter or prettify the entries depending on your needs.

```javascript
import { Window } from 'happy-dom';

const window = new Window();

window.console.log('Test', { test: true });

const entries = window.happyDOM.virtualConsolePrinter.read();
const log = entries.map(entry => entry.message.join(' ')).join('\n');

// Will output 'Test [object Object]' to the NodeJS console
global.console.log(log);
```

## Events

### Print

```javascript
import { Window } from 'happy-dom';

const window = new Window();

window.happyDOM.virtualConsolePrinter.addEventListener('print', () => {
    const log = window.happyDOM.virtualConsolePrinter.readAsString();
    // Will output 'Test {"test": true}' to the NodeJS console
    global.console.log(log);
});

window.console.log('Test', { test: true });
```

### Clear

```javascript
import { Window } from 'happy-dom';

const window = new Window();

window.happyDOM.virtualConsolePrinter.addEventListener('clear', () => {
    // Will clear the NodeJS log
    global.console.clear();
});

window.console.clear();
```

## Use Another Console

It is possible to replace the Virtual Console with another console (such as with the Node.js console).

```javascript
import { Window } from 'happy-dom';

const window = new Window({ console: global.console });

// Will output 'Test' to the Node.js console
window.console.log('Test');
```