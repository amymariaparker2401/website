# 🍰 Рецепти

## React

Спочатку необхідно встановити залежності для React.

[Запис в блозі](http://blog.jakoblind.no/react-parcel/)

```bash
npm install --save react
npm install --save react-dom
npm install --save-dev parcel-bundler
npm install --save-dev babel-preset-env
npm install --save-dev babel-preset-react
```

Або, якщо у вас встановлений менеджер пакетів Yarn

```bash
yarn add react
yarn add react-dom
yarn add --dev parcel-bundler
yarn add --dev babel-preset-env
yarn add --dev babel-preset-react
```

Потім додайте скрипт запуску в `package.json`

```javascript
// package.json
"Scripts": {
  "Start": "parcel index.html"
}
```

## Preact

Спочатку нам потрібно встановити залежності для Preact.

```bash
npm install --save preact
npm install --save preact-compat
npm install --save-dev parcel-bundler
npm install --save-dev babel-preset-env
npm install --save-dev babel-preset-preact
```

 Або, якщо у вас встановлений менеджер пакетів Yarn

```bash
yarn add preact
yarn add preact-compat
yarn add --dev parcel-bundler
yarn add --dev babel-preset-env
yarn add --dev babel-preset-preact
```

Потім переконайтеся, що існує така конфігурація Babel.

```javascript
// .babelrc
{
  "Presets": [ "env", "preact"]
}
```

Потім додайте скрипт запуску в `package.json`

```javascript
// package.json
"Scripts": {
  "Start": "parcel index.html"
}
```

## Vue

Спочатку нам потрібно встановити залежності для Vue.

```bash
npm install --save vue
npm install --save-dev parcel-bundler
```

 Або, якщо у вас встановлений менеджер пакетів Yarn

```bash
yarn add vue
yarn add --dev parcel-bundler
```

Потім додайте скрипт запуску в `package.json`

```javascript
// package.json
"Scripts": {
  "Start": "parcel index.html"
}
```

