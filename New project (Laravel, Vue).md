## Laravel
```
composer create-project laravel/laravel example-app
```

## Vue
```
npm install
npm install vue@next
npm install vue-router@next
npm install vue-loader@next
npm install vue-template-compiler
npm install vuex@next --save
npm install -D sass-loader node-sass
npm install sass resolve-url-loader@^3.1.2 @vue/compiler-sfc --save-dev --legacy-peer-deps
```

## webpack.mix.js
```javascript
const mix = require('laravel-mix');

mix.js('resources/js/app.js', 'public/js')
    .sass('resources/sass/app.scss', 'public/css')
    .vue();

if (mix.inProduction()) {
    mix.version();
}
```

## resources/views/app.blade.php
```html
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">

        <link rel="stylesheet" href="{{ asset('css/app.css') }}">

        <script src="{{ asset('js/app.js') }}" defer></script>

        <title>{{ config('app.name') }}</title>
    </head>
    <body>
        <div id="app"></div>
    </body>
</html>
```

## routes/web.php
```php
Route::get('{any}', function () {
    return view('app');
})->where('any', '.*');
```

## resources/js/app.js
```javascript
import { createApp } from 'vue'

import router from './router'
import { store } from './store';

import App from './components/app/App'

const app = createApp(App)

app.use(router)
app.use(store)
app.mount('#app')
```

## resources/js/router.js
```javascript
import * as VueRouter from 'vue-router';

export default VueRouter.createRouter({
    history: VueRouter.createWebHistory(),
    routes: [
        {
            path: '/',
            name: 'name',
            component: Component,
            children: [
                {
                    path: '',
                    name: 'name',
                    component: Component
                }
            ]
        }
    ]
})
```

## resources/js/store/index.js
```javascript
import { createStore } from "vuex";

export const store = createStore({
    modules: {}
})
```

## resources/js/components/app/App.vue
```html
<template>
    <router-view></router-view>
</template>
```

## resources/sass/app.scss
```scss
.button {
    background-color: white;

    &:active {
        background-color: black;
    }

    &.button--success {
        background-color: green;

        &:hover {
            background-color: yellow;
        }

        @media screen and (max-width: 1300px) {
            background-color: blue;
        }
    }

    &.button--error {
        background-color: red;
    }
}
```

## config/app.php
```text
'locale' => env('APP_LOCALE', 'ru'),
```

## .gitignore
```text
/public/css
/public/js
/public/storage
```
