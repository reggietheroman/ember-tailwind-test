# tailwind-test

Quick project to show use of TailwindCSS inside an [Ember.js v6.5](https://emberjs.com/) application based on [this guide](https://tailwindcss.com/docs/installation/framework-guides/emberjs)

## Pitfalls

### 1. Not including the --embroider flag when generating a new project

```
$ npx ember-cli new my-project --embroider --no-welcome
```
Part of the tailwind configuration requires webpack to configure PostCSS to process your CSS files.

Using the --embroider flag installs
  - [@embroider/compat](https://www.npmjs.com/package/@embroider/compat)
  - [@embroider/core](https://www.npmjs.com/package/@embroider/core)
  - [@embroider/webpack](https://www.npmjs.com/package/@embroider/webpack)

and does away with
  - [ember-cli-sri](https://www.npmjs.com/package/ember-cli-sri)
  - [ember-cli-terser](https://www.npmjs.com/package/ember-cli-terser)

### 2. Not creating an app.css file in the app directory and adding the `@import "tailwindcss";` line to app/styles/app.css instead

```
app
  |-app.css # this is correct
  |_styles
    |_app.css # this is the default that comes with a new emberjs app. Atm, I don't know why this doesn't work
```

---

**Not doing the above will not work if you just follow the steps in the tailwind guide.**
