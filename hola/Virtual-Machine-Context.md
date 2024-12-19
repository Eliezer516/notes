# Virtual Machine Context

The default `Window` class is a NodeJS [VM context](https://nodejs.org/api/vm.html#vm_vm_createcontext_sandbox_options). A [VM context](https://nodejs.org/api/vm.html#vm_vm_createcontext_sandbox_options) will execute JavaScript sandboxed within the context. The Window instance will be the global object within the [VM context](https://nodejs.org/api/vm.html#vm_vm_createcontext_sandbox_options).

```javascript
import { Window } from 'happy-dom';

const window = new Window({
	innerWidth: 1024,
	innerHeight: 768,
	url: 'http://localhost:8080'
});
const document = window.document;

document.write(`
    <html>
        <head>
             <title>Test page</title>
        </head>
        <body>
             <div class="container">
                  <!–– Content will be added here -->
             </div>
            <script>
                const element = document.createElement('div');
                const container = document.querySelector('.container');
                element.innerHTML = 'Test';
                container.appendChild(element);
            </script>
        </body>
    </html>
`);

// Will output "Test"
console.log(document.querySelector('.container div').innerHTML);
```

# Global Context

Happy DOM exports a class called `GlobalWindow`, which can be used to run Happy DOM in the global context instead of the default behaviour of running in a [VM context](https://nodejs.org/api/vm.html#vm_vm_createcontext_sandbox_options).

```javascript
import { Window, GlobalWindow } from 'happy-dom';

const vmWindow = new Window();
const globalWindow = new GlobalWindow();

// Will output "false"
console.log(vmWindow.Array === global.Array);

// Will output "true"
console.log(globalWindow.Array === global.Array);

globalWindow.eval('global.test = 1');

// Will output "1"
console.log(global.test);
```