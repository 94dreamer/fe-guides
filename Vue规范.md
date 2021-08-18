## 前置阅读

- [Vue 官方风格指南](https://cn.vuejs.org/v2/style-guide/)
- [Vant 风格指南](https://youzan.github.io/vant/#/zh-CN/style-guide)

## 规则示例

- **模板属性按顺序排列**

  rule: [`vue/attributes-order`](https://vuejs.github.io/eslint-plugin-vue/rules/attributes-order.html#vue-attributes-order)

  ```xml
  <template>
    <!-- ✓ GOOD -->
    <div
      is="header"
      v-for="item in items"
      v-if="!visible"
      v-once
      id="uniqueID"
      ref="header"
      v-model="headerData"
      my-prop="prop"
      @click="functionCall"
      v-text="textContent"
    >
      test
    </div>
    <div
      v-for="item in items"
      v-if="!visible"
      prop-one="prop"
      :prop-two="prop"
      prop-three="prop"
      @click="functionCall"
      v-text="textContent"
    >
      test
    </div>
    <div
      prop-one="prop"
      :prop-two="prop"
      prop-three="prop"
    >
      test
    </div>

    <!-- ✗ BAD -->
    <div
      ref="header"
      v-for="item in items"
      v-once
      id="uniqueID"
      v-model="headerData"
      my-prop="prop"
      v-if="!visible"
      is="header"
      @click="functionCall"
      v-text="textContent"
    >
      test
    </div>
  </template>
  ```

- **禁止使用 v-html 来防止 XSS 攻击**

  rule: [`vue/no-v-html`](https://vuejs.github.io/eslint-plugin-vue/rules/no-v-html.html#vue-no-v-html)

  ```xml
  <template>
    <!-- ✓ GOOD -->
    <div></div>

    <!-- ✗ BAD -->
    <div v-html="someHTML"></div>
  </template>
  ```

- **组件中的属性按顺序排列**

  rule: [`vue/order-in-components`](https://vuejs.github.io/eslint-plugin-vue/rules/order-in-components.html#vue-order-in-components)

  ```html
  <script>
    /* ✓ GOOD */
    export default {
      name: "app",
      props: {
        propA: Number,
      },
      data() {
        return {
          msg: "Welcome to Your Vue.js App",
        };
      },
    };
  </script>
  ```

  ```html
  <script>
    /* ✗ BAD */
    export default {
      name: "app",
      data() {
        return {
          msg: "Welcome to Your Vue.js App",
        };
      },
      props: {
        propA: Number,
      },
    };
  </script>
  ```

- **禁止在模板中使用 this**

  rule: [`vue/this-in-template`](https://vuejs.github.io/eslint-plugin-vue/rules/this-in-template.html#vue-this-in-template)

  ```xml
  <template>
    <!-- ✓ GOOD -->
    <a :href="url">

    </a>

    <!-- ✗ BAD -->
    <a :href="this.url">

    </a>
  </template>
  ```
