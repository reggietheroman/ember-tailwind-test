### Installation

# Install Tailwind CSS with Ember.js

### Setting up Tailwind CSS in an Ember.js project.

## 01

**Create your project**

Start by creating a new Ember.js project if you don't have one set up already. The most common approach is to use Ember CLI.

#### *Terminal*
```
$ npx ember-cli new my-project --embroider --no-welcome
$ cd my-project
```

## 02

**Install Tailwind CSS**

Using npm, install @tailwindcss/postcss and its peer dependencies, as well as postcss-loader.

#### *Terminal*
```
$ npm install tailwindcss @tailwindcss/postcss postcss postcss-loader
```

## 03

**Enable PostCSS support**

In your ember-cli-build.js file, configure PostCSS to process your CSS files.

#### *ember-cli-build.js*

```
'use strict';
const EmberApp = require('ember-cli/lib/broccoli/ember-app');
module.exports = function (defaults) {
  const app = new EmberApp(defaults, {
    // Add options here
  });
  const { Webpack } = require('@embroider/webpack');
  return require('@embroider/compat').compatBuild(app, Webpack, {
    skipBabel: [
      {
        package: 'qunit',
      },
    ],
    packagerOptions: {
      webpackConfig: {
        module: {
          rules: [
            {
              test: /\.css$/i,
              use: ['postcss-loader'],
            },
          ],
        },
      },
    },
  });
};
```

## 04

**Configure PostCSS Plugins**

Create a postcss.config.mjs file in the root of your project and add the @tailwindcss/postcss plugin to your PostCSS configuration.

#### *postcss.config.mjs*

```
export default {
  plugins: {
    "@tailwindcss/postcss": {},
  },
}
```

## 05

**Import Tailwind CSS**

Create an ./app/app.css file and add an @import for Tailwind CSS.

#### *app.css*

```
@import "tailwindcss";
```

## 06

**Import the CSS file**

Import the newly-created ./app/app.css file in your ./app/app.js file.

#### *app.js*

```
import Application from '@ember/application';
import Resolver from 'ember-resolver';
import loadInitializers from 'ember-load-initializers';
import config from 'my-project/config/environment';
import 'my-project/app.css';
export default class App extends Application {
  modulePrefix = config.modulePrefix;
  podModulePrefix = config.podModulePrefix;
  Resolver = Resolver;
}
loadInitializers(App, config.modulePrefix);
```

## 07

**Start your build process**

Run your build process with npm run start.

#### *Terminal*

```
npm run start
```

## 08

**Start using Tailwind in your project**

Start using Tailwind's utility classes to style your content.

#### *application.hbs*
```
{{page-title "MyProject"}}

<h1 class="text-3xl font-bold underline">
  Hello world!
</h1>

{{outlet}}
```