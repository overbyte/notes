# Using Vue

## Using vim for Editor

Clone `vim-vue` into plugins structure (vim 8 or later)

```
git clone https://github.com/posva/vim-vue.git ~/.vim/pack/plugins/start/vim-vue
```

## Vue CLI

Using vue-cli to set up

```
npm install --global @vue/cli
vue create my-app
```

## Code Style



## JS Components

Usually a vue component will be laid out like this in a `.vue` file:

```
<template></template>
<script></script>
<style module></style>
```

however it may be preferable to use a `.js` es module (if no compilation is
require or just because of personal preference).

To do this, use the `.esm` versions of the vue / vue-router libraries

```
import Vue from 'vue/dist/vue.esm.js';
import VueRouter from 'vue-router/dist/vue-router.esm.js';
```

## Routing

`vue-cli` sets up a `/router/index.js` for routing.

```
import Vue from 'vue/dist/vue.esm.js';
import VueRouter from 'vue-router/dist/vue-router.esm.js';
import MyView from '../views/MyView';
import Section1 from '../views/Section1';
import Section2 from '../views/Section2';

Vue.use(VueRouter);

const routes = [
    {
        path: '/',
        name: 'Home',
        component: Home,
    },
    {
        path: '/section',
        name: 'Home',
        component: Home,
        children: [
            {
                path: 'sec1',
                name: 'Section 1',
                component: Section1
            },
            {
                path: 'sec2',
                name: 'Section 2',
                component: Section2
            },
        ]
    },
    {
        path: '*',
        redirect: '/',
    },
];

const router = new VueRouter({
    mode: 'history',
    base: process.env.BASE_URL,
    routes
});

export default router;
```

Notes:

* `path: '*'` is a catch-all to either show a 404 or (in this case) redirect
* `children` allows router to nest routes within views

In the `main.js`

```
import Vue from 'vue/dist/vue.esm.js';
import router from './router';
import App from './App';

Vue.config.productionTip = false;

new Vue({
  router,
  render: h => h(App)
}).$mount('#app');
```

## Using css modules

In order to stop css polluting other modules / libraries, we can create css
modules which are scoped to the component that uses them:

* name the style `MyComponent.module.css`
* in `MyComponent.js`:

```
import style from './MyComponent.module.css';

export default {
    data() {
        return { style };
    },
    template: `
<div :class="style.my-component">
    <h1>MyComponent</h1>
</div>
    `,
};
```

Notes:

* import as a variable (in this case, `style`)
* return variable `style` in `data()` to allow the component to use it
* use dynamic classname from `style` var
