[![Published on NPM](https://img.shields.io/npm/v/@polymer/iron-doc-viewer.svg)](https://www.npmjs.com/package/@polymer/iron-doc-viewer)
[![Build status](https://travis-ci.org/PolymerElements/iron-doc-viewer.svg?branch=master)](https://travis-ci.org/PolymerElements/iron-doc-viewer)
[![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg)](https://beta.webcomponents.org/element/PolymerElements/iron-doc-viewer)

## &lt;iron-doc-viewer&gt;

A collection of elements that display documentation about custom elements,
mixins, classes, and more using the JSON descriptor format produced by [Polymer
Analyzer](https://github.com/Polymer/polymer-analyzer).

See:
[Documentation](https://www.webcomponents.org/element/@polymer/iron-doc-viewer),
[Demo](https://www.webcomponents.org/element/@polymer/iron-doc-viewer/demo/demo/index.html).

You may also be interested in
[`<iron-component-page>`](https://github.com/PolymerElements/iron-component-page),
which composes the iron-doc elements into a more complete documentation
browser.

### Elements

* `<iron-doc-nav>` Show a table-of-contents.
* `<iron-doc-viewer>` Manage routing and delegate to a child doc element.
* `<iron-doc-element>` Show docs about a custom element.
* `<iron-doc-behavior>` Show docs about a Polymer behavior.
* `<iron-doc-namespace>` Show docs about a JavaScript namespace.
* `<iron-doc-class>` Show docs about a JavaScript class.
* `<iron-doc-mixin>` Show docs about a JavaScript mixin.

## Usage

### Installation
```
npm install --save @polymer/paper-input
```

### In an html file
```html
<html>
  <head>
    <script type="module">
      import '@polymer/polymer/lib/elements/dom-bind.js';
      import '@polymer/iron-ajax/iron-ajax.js';
      import '@polymer/iron-doc-viewer/iron-doc-viewer.js';
    </script>
  </head>

  <body>
    <dom-bind>
      <template>
        <iron-ajax
          auto
          url="./analysis.json"
          last-response="{{descriptor}}">
        </iron-ajax>

        <iron-doc-viewer
          descriptor="[[descriptor]]"
          root-namespace="MyNamespace">
        </iron-doc-viewer>
      </template>
    </dom-bind>
  </body>
</html>
```

### In a Polymer 3 element
```js
import {PolymerElement, html} from '@polymer/polymer';
import '@polymer/iron-doc-viewer/iron-doc-viewer.js';

class SampleElement extends PolymerElement {
  static get template() {
    return html`
      <iron-doc-viewer
        descriptor="[[descriptor]]"
        root-namespace="MyNamespace">
      </iron-doc-viewer>
    `;
  },

  static get properties() {
    return {
      descriptor: {
        type: Object,
        value: {
          // Analyzer descriptor goes here.
        }
      }
    };
  }
}

customElements.define('sample-element', SampleElement);
```

### Routing

`<iron-doc-viewer>` handles URL routing to provide permanent addresses for all
locations in the documentation tree, including scroll anchor targets.

By default it uses the URL fragment for routing (e.g.
`docs.html#/elements/my-element#property-foo`), in order to support simple
static file hosts.

To use the real URL path for routing, set the `base-href` property to the
server mount point, omitting the trailing slash (e.g. `/api/docs` or *empty
string* for the root path). Note that this requires a host that serves the
application from all paths that should be handled by the doc viewer.

### Styling

The iron-doc elements come with an optional material-design default theme that
must be explicitly included as custom style:

```html
<script type="module">
  import '@polymer/iron-doc-viewer/default-theme.js';
</script>

<custom-style>
  <style is="custom-style" include="iron-doc-default-theme"></style>
</custom-style>
```

The following custom properties and mixins are available for styling:

Custom property | Description | Default
----------------|-------------|----------
`--iron-doc-accent-color` | Color for emphasis (e.g. hyperlink hover). | `#1565c0`
`--iron-doc-font-body` | Mixin applied to non-code text. | `{}`
`--iron-doc-font-code` | Mixin applied to code snippets. | `{}`
`--iron-doc-title` | Mixin applied to page titles. | `{}`
`--iron-doc-heading` | Mixin applied to section headings. | `{}`

## Contributing
If you want to send a PR to this element, here are
the instructions for running the tests and demo locally:

### Installation
```sh
git clone https://github.com/PolymerElements/iron-doc-viewer
cd paper-input
npm install
npm install -g polymer-cli
```

### Running the demo locally
```sh
polymer serve --npm
open http://127.0.0.1:<port>/demo/
```

### Running the tests
```sh
polymer test --npm
```
