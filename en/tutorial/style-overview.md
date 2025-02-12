{{target: style-overview}}

# Overview of Style Customization

This article provides an overview of the different approaches about style customization. For example, how to config the color, size, shadow of the graphic elements and labels.

> The term "style" may not follow the convention of data visualization, but we use it in this article because it is popular and easy to understand.

These approaches below will be introduced. The functionalities of them might be overlapped, but they are suitable for different scenarios.

+ Theme
+ Pallette
+ Customize style explicitly (itemStyle, lineStyle, areaStyle, label, ...)
+ Visual encoding (visualMap component)

Other article about styling can be check in [Customized Chart Styles](~Customized%20Chart%20Styles) and [Visual Map of Data](~Visual%20Map%20of%20Data).


<br>

---

<br>

**Theme**

Setting a theme is the simplest way to change the color style. For example, in [Examples page](https://ecomfe.github.io/echarts-examples/public/index.html), "Theme" can be selected, and view the result directly.

Since ECharts4, besides the original default theme, ECharts provide another two built-in themes, named '`'light'` and `'dark'`. They can be used as follows:

```js
var chart = echarts.init(dom, 'light');
```

或者

```js
var chart = echarts.init(dom, 'dark');
```

Other themes are not included in ECharts package by default, and need to load them ourselves if we want to use them. Themes can be visited and downloaded in [Theme Builder](http://echarts.baidu.com/theme-builder/). Theme can also be created or edited in it. The downloaded theme can be used as follows:

If a theme is downloaded as a JSON file, we should register it by ourselves, for example:
```js
var xhr = new XMLHttpRequest();
// Assume the theme name is "vintage".
xhr.open('GET', 'xxx/xxx/vintage.json', true);
xhr.onload = function () {
    var themeJSON = this.response;
    echarts.registerTheme('vintage', JSON.parse(themeJSON))
    var chart = echarts.init(dom, 'vintage');
    // ...
});
xhr.send();
```

If a them is downloaded as a JS file, it will auto register itself:
```js
// Import the `vintage.js` file in HTML, then:
var chart = echarts.init(dom, 'vintage');
// ...
```

<br>

---

<br>

**Palette**

Pallettes can be given in option. They provide a group of colors, which will be auto picked by series and data. We can give a global palette, or exclusive pallette for certain series.

```js
option = {
    // Global palette:
    color: ['#c23531','#2f4554', '#61a0a8', '#d48265', '#91c7ae','#749f83',  '#ca8622', '#bda29a','#6e7074', '#546570', '#c4ccd3'],

    series: [{
        type: 'bar',
        // A palette only work for the series:
        color: ['#dd6b66','#759aa0','#e69d87','#8dc1a9','#ea7e53','#eedd78','#73a373','#73b9bc','#7289ab', '#91ca8c','#f49f42'],
        ...
    }, {
        type: 'pie',
        // A palette only work for the series:
        color: ['#37A2DA', '#32C5E9', '#67E0E3', '#9FE6B8', '#FFDB5C','#ff9f7f', '#fb7293', '#E062AE', '#E690D1', '#e7bcf3', '#9d96f5', '#8378EA', '#96BFFF'],
        ...
    }]
}
```


<br>

---

<br>

**Customize style explicitly (itemStyle, lineStyle, areaStyle, label, ...)**

It is a common way to set style explicitly. Throughout ECharts [option](option.html), style related options can be set in various place, including [itemStyle](option.html#series.itemStyle), [lineStyle](option.html#series-line.lineStyle), [areaStyle](option.html#series-line.areaStyle), [label](option.html#series.label), etc.

Generally speaking, all of the built-in components and series follow the naming convention like `itemStyle`, `lineStyle`, `areaStyle`, `label` etc., although they may occur in different place according to different series or components.

There is another article for style setting, [Customized Chart Styles](~Customized%20Chart%20Styles).



<br>

---

<br>

**Style of emphasis state**

When mouse hovering a graphic elements, usually the emphasis style will be displayed. By default, the emphasis style is auto generated by the normal style. However they can be specified by [emphasis](option.html#series-scatter.emphasis) property. The options in [emphasis](option.html#series-scatter.emphasis) is the same as the ones for normal state, for example:

```js
option = {
    series: {
        type: 'scatter',

        // Styles for normal state.
        itemStyle: {
            // Color of the point.
            color: 'red'
        },
        label: {
            show: true,
            // Text of labels.
            formatter: 'This is a normal label.'
        },

        // Styles for emphasis state.
        emphasis: {
            itemStyle: {
                // Color in emphasis state.
                color: 'blue'
            },
            label: {
                show: true,
                // Text in emphasis.
                formatter: 'This is a emphasis label.'
            }
        }
    }
}
```

Notice: Before ECharts4, the emphasis style should be written like this:

```js
option = {
    series: {
        type: 'scatter',

        itemStyle: {
            // Styles for normal state.
            normal: {
                color: 'red'
            },
            // Styles for emphasis state.
            emphasis: {
                color: 'blue'
            }
        },

        label: {
            // Styles for normal state.
            normal: {
                show: true,
                formatter: 'This is a normal label.'
            },
            // Styles for emphasis state.
            emphasis: {
                show: true,
                formatter: 'This is a emphasis label.'
            }
        }
    }
}
```

The option format is still **compatible**, but not recommended. In fact, in most cases, users only set normal style, and use the default emphasis style. So since ECharts4, we support to write style without the "normal" term, which makes the option more simple and neat.


<br>

---

<br>

**Visual encoding (visualMap component)**

[visualMap component](option.html#visualMap) supports config the rule that mapping value to visual channel (color, size, ...). More details can be check in [Visual Map of Data](~Visual%20Map%20of%20Data).
