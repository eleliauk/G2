---
title: wordCloud
order: 27
---

`wordCloud` 是一种专门用于生成词云图的工具。词云图是一种直观展示文本数据中关键词频次的可视化形式，通过不同大小、颜色和位置的文字来反映词语的重要性或权重。

使用 `wordCloud` 组件时，用户可以轻松地将文本数据转化为视觉化的词云图。支持高度自定义的配置选项，包括文字大小范围、颜色映射、旋转角度以及布局算法等，从而满足多样化的可视化需求。此外，`wordCloud` 还能够与 G2 的其他功能无缝集成，例如数据筛选、交互事件绑定等，进一步增强用户体验。

无论是用于展示社交媒体热点话题、分析用户评论情感，还是呈现关键词分布，`wordCloud` 都能以优雅的方式帮助用户快速洞察数据背后的趋势和模式。`wordCloud` 不仅简单易用，还具备出色的性能表现，是数据可视化领域的理想选择之一。

## 开始使用

```js | ob
(() => {
  const chart = new G2.Chart();

  chart.options({
    type: 'wordCloud', // 指定图表类型为词云图
    data: {
      type: 'fetch',
      value: 'https://assets.antv.antgroup.com/g2/philosophy-word.json',
    },
    layout: {
      spiral: 'rectangular', // 词云布局模式：矩形螺旋布局（可选 'archimedean' 阿基米德螺旋布局）
    },
    encode: { color: 'text' }, // 将数据字段 `text` 映射到词云图的颜色
    legend: false, // 关闭图例显示
    axis: false, // 关闭坐标轴显示
    tooltip: false, // 关闭tooltip
  });

  chart.render();

  return chart.getContainer();
})();
```

更多的案例，可以查看[图表示例 - 文本](/examples#general-text)页面。

## 配置项

| 属性   | 描述                                                                                                   | 类型              | 默认值 | 必选 |
| ------ | ------------------------------------------------------------------------------------------------------ | ----------------- | ------ | ---- |
| encode | 配置 `wordCloud` 标记的视觉通道，包括`x`、`y`、`color`、`size`等，用于指定视觉元素属性和数据之间的关系 | [encode](#encode) | -      | ✓    |
| scale  | 配置 `wordCloud` 标记的图形缩放，包括`x`、`y`、`series`、`size`等                                      | [scale](#scale)   | -      |      |
| style  | 配置 `wordCloud` 图形样式                                                                              | [style](#style)   | -      |      |
| layout | 布局配置                                                                                               | [layout](#style)  | -      |
| labels | 自定义节点数据标签的配置                                                                               | `label[]`         | `[]`   |

### encode

配置 `wordCloud` 标记的视觉通道，定义数据字段与视觉属性之间映射关系的重要配置，它决定了数据如何转化为视觉表现。

| 属性     | 描述                                                                       | 类型                          | 默认值     | 必选 |
| -------- | -------------------------------------------------------------------------- | ----------------------------- | ---------- | ---- |
| x        | 绑定 `wordCloud` 标记的 `x` 属性通道，一般是 `data` 中的时间或有序名词字段 | [encode](/manual/core/encode) | `'x'`      |      |
| y        | 绑定 `wordCloud` 标记的 `y` 属性通道，一般是 `data` 中的数值或数组字段     | [encode](/manual/core/encode) | `'y'`      |      |
| text     |                                                                            | [encode](/manual/core/encode) | `'text'`   |      |
| rotate   |                                                                            | [encode](/manual/core/encode) | `'rotate'` |      |
| fontSize |                                                                            | [encode](/manual/core/encode) | `'size'`   |      |
| shape    |                                                                            | [encode](/manual/core/encode) | `'tag'`    |      |
更多的`encode`配置，可以查查看 [encode](/manual/core/encode) 介绍页面。


### scale

`scale`用于定义数据如何映射到视觉属性（如颜色、大小、形状等）。在`cell`的使用场景，scale 的常见作用就是为每个视觉通道（如颜色、大小、位置等）提供映射规则，使数据点能够准确地呈现。

| 属性 | 描述                                  | 类型                                        | 默认值              | 必选 |
| ---- | ------------------------------------- | ------------------------------------------- | ------------------- | ---- |
| x    | 定义数据字段到 X 轴视觉位置的映射规则 | Record<string, [scale](/manual/core/scale)> | `{ range: [0, 1] }` |      |
| y    | 定义数据字段到 X 轴视觉位置的映射规则 | Record<string, [scale](/manual/core/scale)> | `{ range: [0, 1] }` |      |


更多的`scale`配置，可以查查看 [scale](/manual/core/scale) 介绍页面。


### layout 

| 属性      | 描述         | 类型                             | 默认值 |
| --------- | ------------ | -------------------------------- | ------ |
| padding   | 内间距       | `number`                         | `1`    |
| rotate    | 文字旋转角度 | `number` \| `word => number`     | -      |
| random    | 随机方式     | `number` \| `word => number`     | -      |
| spiral    | 外观图形     | `'archimedean' \| 'rectangular'` | -      |
| imageMask | 图片蒙层     | `'HTMLImageElement \| string`    | -      |

### style

复合图形标记需要通过不同的前缀来区分图形的配置。

- `<label>`: 数据标签的前缀，例如：`labelText` 设置标签的 text 文本。


1	| 属性 | 描述 | 类型 | 默认值 | 必选 |
2	| ---------------------- | ------------------------ | ------------------------------------------------------------ | --------- | ---- |
3	| wordcloudSize | 词云大小 | number \| (datum, index, data) => number | - | |
4	| wordcloudFill | 词云填充颜色 | string \| (datum, index, data) => string | - | |
5	| wordcloudFillOpacity | 词云填充透明度 | number \| (datum, index, data) => number | - | |
6	| wordcloudStroke | 词云描边颜色 | string \| (datum, index, data) => string | - | |
7	| wordcloudStrokeOpacity | 词云描边透明度 | number \| (datum, index, data) => number | - | |
8	| wordcloudLineWidth | 词云描边宽度 | number \| (datum, index, data) => number | - | |
9	| wordcloudLineDash | 词云描边虚线配置 | [number,number] \| (datum, index, data) => [number , number] | - | |
10	| wordcloudOpacity | 词云整体透明度 | number \| (datum, index, data) => number | - | |
11	| wordcloudShadowColor | 词云阴影颜色 | string \| (datum, index, data) => string | - | |
12	| wordcloudShadowBlur | 词云阴影模糊系数 | number \| (datum, index, data) => number | - | |
13	| wordcloudShadowOffsetX | 词云阴影水平偏移 | number \| (datum, index, data) => number | - | |
14	| wordcloudShadowOffsetY | 词云阴影垂直偏移 | number \| (datum, index, data) => number | - | |
15	| wordcloudCursor | 词云鼠标样式 | string \| (datum, index, data) => string | `default` | |