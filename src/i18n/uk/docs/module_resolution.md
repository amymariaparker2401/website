# 📔 Дозволи модулів

Parcel \(v1.7.0 і вище\) підтримує декілька стратегій дозволу модуля з коробки, так що вам не доведеться мати справу з нескінченними відносними шляхами `../../`.

Примітки:

* **project root**: каталог точки входу, зазначеної для Parcel, або спільний корінь \(загальний батьківський каталог\), якщо зазначено декілька точок входу.
* **package root**: каталог найближчого кореня модуля `node_modules`.

## Абсолютний шлях

`/foo` буде `foo` по відношенню до **project root**.

## ~ Tilde Paths

`~/foo` буде означати `foo` відносно найближчого **package root** або, якщо не знайдено, **project root**.

## Aliasing

Псевдоніми підтримуються через поле `alias` у `package.json`.

Цей приклад псевдонімів `react` в `preact` і деякий місцевий користувацький модуль, в якому немає `node_modules`.

```javascript
// package.json
{
  "name": "some-package",
  "devDependencies": {
    "parcel-bundler": "^1.7.0"
  },
  "alias": {
    "react": "preact-compat",
    "react-dom": "preact-compat",
    "local-module": "./custom/modules"
  }
}
```

Уникайте використання будь-яких спеціальних символів у ваших псевдонімах, оскільки деякі з них можуть використовуватися Parcel та іншими засобами сторонніх інструментів або розширень. Наприклад:

* `~` використовується Parcel для вирішення [tilde paths](module_resolution.md#~-tilde-paths).
* `@` використовується npm для вирішення npm організацій.

Ми радимо бути чітко визначеними вашими псевдонімами, тому будь ласка **вкажіть розширення файлів**, інакше Parcel доведеться вгадати. Дивіться [JavaScript Named Exports](module_resolution.md#JavaScript-Named-Exports) для прикладу цього.

## Інші умови

### JavaScript Named Exports

Списки псевдонімів застосовуються до багатьох типів ресурсів і не підтримують спеціальне відображення JavaScript-експорту. Якщо ви хочете вказати назву експорту JS, ви можете зробити це:

```javascript
// package.json
{
  "name": "some-package",
  "alias": {
    "ipcRenderer": "./electron-ipc.js" // вкажіть розширення файлу
  }
}
```

і повторно експортуйте назву експорту в псевдонімний файл:

```javascript
// electron-ipc.js
module.exports = require('electron').ipcRenderer
```

### TypeScript ~ Resolution

TypeScript повинен знати про те, що ви використовуєте `~` модуль або відображення псевдоніма. Будь ласка, зверніться до [TypeScript Module Resolution docs](https://www.typescriptlang.org/docs/handbook/module-resolution.html) для додаткової інформації.

```javascript
// tsconfig.json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "~*": ["./src/*"]
    }
  }
}
```

### Monorepo Resolution

Це рекомендовані звичаї з Monorepo в цей час:

Рекомендується використання:

* використовувати відносні шляхи.
* використовуйте `/` для кореневого шляху, якщо потрібно корінь.

Неприйнятне використання:

* **avoid** `~` використовувати з monorepos.

Якщо ви є користувачем monorepos і хотіли б внести свій внесок у ці рекомендації, будь ласка, наведіть приклади репозиторіїв при відкритті питань для підтримки обговорення.

