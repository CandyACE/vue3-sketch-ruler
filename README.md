# vue3-sketch-ruler

> 此版本只在vue3中使用,用于页面展示的缩放操作, 最新版本为2X master 分支, 如果需要学习vue-demi关于vue2/vue3通用组件的, 请切换到1x分支

[![](https://camo.githubusercontent.com/28479a7a834310a667f36760a27283f7389e864a/68747470733a2f2f696d672e736869656c64732e696f2f6e706d2f6c2f76322d646174657069636b65722e737667)](https://camo.githubusercontent.com/28479a7a834310a667f36760a27283f7389e864a/68747470733a2f2f696d672e736869656c64732e696f2f6e706d2f6c2f76322d646174657069636b65722e737667) [![build status](https://github.com/kakajun/vue3-sketch-ruler/actions/workflows/gh-pages.yml/badge.svg?branch=master)](https://github.com/kakajun/vue3-sketch-ruler/actions/workflows/gh-pages.yml)

## 🚀 Features

- 💪 Vue 3 Composition API
- 🔥 Written in TypeScript
- 🔋 SSR Friendly
- 💡 以鼠标为中心缩放页面
- 📦 减化配置
- 💎 提供还原, 放大, 缩小的功能

# Vue 3 + Vite + ts 打包sketchRuler

## 说明

---

插件应用范围: 适合作为低代码平台操作页面缩放工具,比如做图工具如, 大屏可视化, 做图工具图怪兽等,类似ps的缩放效果.

<!-- 应用案例: [avue大屏可视化工具](https://data.avuejs.com/build/1) ![image](https://github.com/kakajun/vue3-sketch-ruler/blob/1x/example/v2/assets/dp.png) -->

## ✨ 升级改造

1. 在原来1X版本中满足基本的缩放和标注辅助线的功能, 但是缩放时, 是固定以画面左上角位缩放点, 这样子在实际操作中会很不方便，所以这里对缩放功能进行了改进，以鼠标为中心缩放页面，这样在操作中会更方便。
2. 对辅助线做了调整, 减少了细刻度的绘制, 因为已经有刻度显示, 删除后画面更加简洁
3. 辅助线位置显示跟随鼠标移动
4. 删除辅助线是以拖拽线条到编辑框外即可
5. 新增还原, 放大, 缩小的API
6. 修改引用方式, 减少繁琐的配置

升级过程简单写了一篇掘金文章, 同行或感兴趣的可以留言交流

[掘金:大屏页面缩放插件---升级改造](https://juejin.cn/post/7025195450080690212)

## demo

案例浏览: [https://kakajun.github.io/vue3-sketch-ruler](https://kakajun.github.io/vue3-sketch-ruler) ![image](https://github.com/kakajun/vue3-sketch-ruler/blob/master/example/assets/newDemo.png)

## 安装

> 支持全局导入和模块导入

```js
npm install --save vue3-sketch-ruler

yarn add vue3-sketch-ruler  -S
```

## 引入方式

将打包后的dist包拷贝，用import导入，支持下面两种引用方式

```
import { SketchRule } from 'vue3-sketch-ruler'
import 'vue3-sketch-ruler/lib/style.css'

 components: { SketchRule }
```

也可以是这样子

```
import SketchRule from 'vue3-sketch-ruler'
import 'vue3-sketch-ruler/lib/style.css'

 components: SketchRule
```

## 支持的功能

- [x] 标尺渲染
- [x] 缩放内容，重绘标尺
- [x] 滚动内容，重绘标尺
- [x] 切换标尺状态，显示或隐藏
- [x] 参考线管理（增加删除）
- [x] 支持参考线任意地方拖拽
- [x] 左上角的眼睛，点击能控制红线显影
- [x] 提供右下角按钮缩放,还原所需API

## 未来支持的功能

- [] 缩放导航功能
- [] 加入单元测试功能

这是个开源业余做的功能，有兴趣加强该插件的小伙伴欢迎加入，也欢迎大家提pr或者issue

## 使用

```
<SketchRule
  :thick="state.thick"
  v-model:scale="state.scale"
  :width="rectWidth"
  :height="rectHeight"
  :startNumX="0"
  :endNumX="canvasWidth"
  :startNumY="0"
  :endNumY="canvasHeight"
  ref="sketchrule"
  :isShowReferLine="state.isShowReferLine"
  @onCornerClick="handleCornerClick"
  :lines="state.lines"
>
  <template #default>
    <div data-type="page" :style="canvasStyle">
      <img class="img-style" :src="bgImg" alt="" />>
    </div>
  </template>
  <template #btn="{ resetMethod, zoomInMethod, zoomOutMethod }">
    <div class="btns">
      <button class="btn reset-btn" @click="resetMethod">还原</button>
      <button class="btn zoomin-btn" @click="zoomInMethod">放大</button>
      <button class="btn zoomout-btn" @click="zoomOutMethod">缩小</button>
    </div>
  </template>
</SketchRule>

import Vue from 'vue';
import {SketchRule} from "vue-sketch-ruler";
import 'vue3-sketch-ruler/lib/style.css'
const rectWidth = 1200
const rectHeight = 600
const canvasWidth = 800
const canvasHeight = 400

```

参考一个完整的例子，[点击这里](https://github.com/kakajun/vue3-sketch-ruler/blob/master/example/components/user-rulerts.vue)

## api

### 属性

| 属性名称     | 描述                      | 类型          | 默认值      |
| ------------ | ------------------------- | ------------- | ----------- |
| scale        | 初始化标尺的缩放          | Number        | 2           |
| thick        | 标尺的厚度                | Number        | 16          |
| width        | 放置标尺窗口的宽度        | Number        | -           |
| height       | 放置标尺窗口的高度        | Number        | -           |
| eyeIcon      | 睁眼图标                  | String        | -           |
| closeEyeIcon | 闭眼图标                  | String        | -           |
| startNumX    | x轴标尺刻度开始的坐标数值 | Number        | -Infinity   |
| endNumX      | x轴标尺刻度结束的坐标数值 | Number        | Infinity    |
| startNumY    | Y轴标尺刻度开始的坐标数值 | Number        | -Infinity   |
| endNumY      | Y轴标尺刻度结束的坐标数值 | Number        | Infinity    |
| lines        | 初始化水平标尺上的参考线  | object<Array> | {h:[],v:[]} |
| palette      | 标尺的样式配置参数        | Palette       | 如下        |

palette:{bgColor: 'rgba(225,225,225, 0)',longfgColor: '#BABBBC',fontColor: '#7D8694', shadowColor: '#E8E8E8',lineColor: '#EB5648', borderColor: '#DADADC',cornerActiveColor: 'rgb(235, 86, 72, 0.6)',}

### 更新说明

### Event

| 事件名称      | 描述           | 回调参数 |
| ------------- | -------------- | -------- |
| onCornerClick | 左上角点击事件 |          |

### 插槽提供方法

| 事件名称     | 描述         | 回调参数 |
| ------------ | ------------ | -------- |
| resetMethod  | 画布重置位置 |          |
| zoomInMethod | 画布放大     |          |
| zoomInMethod | 画布缩小     |          |

## 引用

vue标尺组件 [vue-sketch-ruler](https://github.com/chuxiaoguo/vue-sketch-ruler.git)
