# Server Side Rendering

## Web Components

Happy DOM supports rendering custom elements (web components) server-side using a new web feature called [Declarative Shadow DOM](https://chromestatus.com/feature/5191745052606464).

[Declarative Shadow DOM](https://chromestatus.com/feature/5191745052606464) is only supported by Chromium based browsers. Unsupported browsers will safely fallback to being rendered using client side Javascript.

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
            <div>
                <my-custom-element>
                    <span>Slotted content</span>
                </my-custom-element>
            </div>
            <script>
                class MyCustomElement extends HTMLElement {
                    constructor() {
                        super();
                        this.attachShadow({ mode: 'open' });
                    }

                    connectedCallback() {
                        this.shadowRoot.innerHTML = \`
                            <style>
                                :host {
                                    display: inline-block;
                                    background: red;
                                }
                            </style>
                            <div><slot></slot></div>
                        \`;
                    }
                }

                customElements.define('my-custom-element', MyCustomElement);
            </script>
        </body>
    </html>
`);

/*
Will output:
<my-custom-element>
    <span>Slotted content</span>
    <template shadowroot="open">
        <style>
            :host {
                display: inline-block;
                background: red;
            }
        </style>
        <div><slot></slot></div>
    </template>
</my-custom-element>
*/
console.log(document.body.querySelector('div').getInnerHTML({ includeShadowRoots: true }));
```