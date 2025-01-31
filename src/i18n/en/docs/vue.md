# Vue

_Supported extensions: `vue`_

Vue.js is a progressive, incrementally-adoptable JavaScript framework for building UI on the web. Parcel supports Vue right out of the box without the need for any additional configuration.

```markup
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Parcel - Vue</title>
  </head>
  <body>
    <div id="app"></div>
    <script src="./index.js"></script>
  </body>
</html>
```

You can use all tools you like \(Pug, TypeScript, SCSS, ...\):

```text
// app.vue
<template lang="pug">
  .container Hello {{bundler}}
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  data() {
    return {
      bundler: "Parcel"
    };
  }
});
</script>

<style lang="scss" scoped>
.container {
  color: green;
}
</style>
```

```javascript
// index.js
import Vue from 'vue';
import App from './app.vue';

new Vue(App).$mount('#app')
```

