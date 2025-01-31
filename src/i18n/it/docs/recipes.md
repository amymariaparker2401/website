# 🍰 Ricette

## React

Come prima cosa installa le dipendenze di React

[Vedi Post](http://blog.jakoblind.no/react-parcel/)

```bash
npm install --save react
npm install --save react-dom
npm install --save-dev parcel-bundler
```

Oppure, se si vuole utilizzare Yarn

```bash
yarn add react
yarn add react-dom
yarn add --dev parcel-bundler
```

Aggiungi uno script di Start nel `package.json`

```javascript
// package.json
"scripts": {
  "start": "parcel index.html"
}
```

## Preact

Come prima cosa installa le dipendenze di Preact

```bash
npm install --save preact
npm install --save preact-compat
npm install --save-dev parcel-bundler
npm install --save-dev babel-preset-env
npm install --save-dev babel-preset-preact
```

Oppure, se si vuole utilizzare Yarn

```bash
yarn add preact
yarn add preact-compat
yarn add --dev parcel-bundler
yarn add --dev babel-preset-env
yarn add --dev babel-preset-preact
```

Poi assicurati che questa configurazione di Babel sia presente.

```javascript
// .babelrc
{
  "presets": ["env", "preact"]
}
```

Aggiungi uno script di Start nel `package.json`

```javascript
// package.json
"scripts": {
  "start": "parcel index.html"
}
```

## Vue

Come prima cosa installa le dipendenze di Vue

```bash
npm install --save vue
npm install --save-dev parcel-bundler
```

Oppure, se si vuole utilizzare Yarn

```bash
yarn add vue
yarn add --dev parcel-bundler
```

Aggiungi uno script di Start nel `package.json`

```javascript
// package.json
"scripts": {
  "start": "parcel index.html"
}
```

