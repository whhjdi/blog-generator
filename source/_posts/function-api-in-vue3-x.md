---
title: function-api-in-vue3.x
date: 2019-06-12 16:55:53
tags: [vue]
cover_img:
feature_img:
description:
keywords:
---

## vue3.x

[vueconf 尤雨溪的演讲视频及资料](https://www.yuque.com/vueconf/2019/gwn1z0#Mit9a)

前几天的 vueconf 大会，尤大介绍了一些 vue3.x 的新的东西，最重要的就是取消了 class api 提案，采用了 function api,
下面是详细的介绍

[尤大在知乎上对 Vue Function-based API RFC 的详细介绍](https://zhuanlan.zhihu.com/p/68477600)

### 基础的例子

感觉有点像 react hooks,但是又不一样

```js
import { value, computed, watch, onMounted } from "vue";
const App = {
  template: `
    <div>
      <span>count is {{ count }}</span>
      <span>plusOne is {{ plusOne }}</span>
      <button @click="increment">count++</button>
    </div>
    `,
  setup() {
    // value : reactive state
    //创建一个变量count,初始值是0
    //模板中使用 `count` 不需要  `count.value`
    const count = value(0);

    // computed : 计算属性
    //创建一个变量plusOne,他的值是根据count的value计算而来的
    const plusOne = computed(() => count.value + 1);

    //methods : 方法
    const increment = () => {
      count.value + 1;
    };

    //watch
    //监听count值得变化，并把count的值 *2 传给回调函数，当count变化的时候调用回调函数
    watch(
      () => count.value * 2,
      val => {
        console.log(`count is ${val}`);
      }
    );

    //生命周期
    onMounted(() => {
      console.log(`mounted`);
    });

    return {
      count,
      plusOne,
      increment
    };
  }
};
```

期待年底的 vue3.0
