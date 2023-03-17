# vue3-study
vue3学习项目，《vuejs设计与实现》阅读笔记。

## 一、框架设计核心要素
1. 提供友好的警告信息，可以通过编写自定义formatter来自定义log的输出形式。（Vue3源码中的 initCustomFormatter）。
2. 利用如 __DEV__ 这种变量来作为警告输出的条件，这样在打包生产环境资源的时候警告信息代码会被认为是 dead code，从而被打包工具移除。
3. 做好 Tree-Shaking，以下注释可以告诉打包工具这段代码不会产生副作用，可以放心移除。
    ```js
    /*#__PURE__*/
    ```
4. 前端需要根据环境、使用场景来输出不同形式的产物：
    - 直接在script中导入，使用 iife 格式
    - 支持 `<script type="module"></script>` 中导入，使用 esm 格式。esm格式还需要注意需要分两种，一种是给 webpack/rollup 等打包工具使用的，另一种是直接给 script 标签使用的，它们的区别的环境变量的判断
    - 需要提供给nodejs使用，场景是服务端渲染

