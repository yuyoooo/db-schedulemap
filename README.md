# db-schedulemap

> 用于渲染赛程图的包，使用DOM渲染

## 安装

``` bash
# install dependencies -S
npm install db-schedulemap

# install node-sass sass-loader  依赖
npm install node-sass sass-loader

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```


## 参数
名称 | 作用 | 类型 | 默认
--|:--:|:--:|:--:
title|标题|String|赛程图
show|列标题|Boolean|true
info|渲染数据|Array|[]
config|样式设置|Object|如下

### 

### info

#### 数据格式

```js
[
	{
		title: "8进4",// 标题
		list:[
            [
              {
                name: "EDG",// 名称
                win: true,// 胜负
                id: 1,
              },
              {
                name: "DWG",
                win: false,
                id: 2,
              },
            ],
          ],
	}
]
```

#### 例子：

![./src/assets/show.png]()

```js
[
        {
          title: "8进4",// 标题
          list: [
            [
              {
                name: "EDG",
                win: true,
                id: 1,
              },
              {
                name: "RNG",
                win: false,
                id: 2,
              },
            ],
            [
              {
                name: "IG",
                win: true,
                id: 1,
              },
              {
                name: "JDG",
                win: false,
                id: 2,
              },
            ],
            [
              {
                name: "DWG",
                win: true,
                id: 1,
              },
              {
                name: "T1",
                win: false,
                id: 2,
              },
            ],
            [
              {
                name: "VG",
                win: true,
                id: 1,
              },
              {
                name: "TES",
                win: false,
                id: 2,
              },
            ],
          ],
        },
        {
          title: "4进2",
          list: [
            [
              {
                name: "EDG",
                win: true,
                id: 1,
              },
              {
                name: "IG",
                win: false,
                id: 2,
              },
            ],
            [
              {
                name: "DWG",
                win: true,
                id: 1,
              },
              {
                name: "VG",
                win: false,
                id: 2,
              },
            ],
          ],
        },
        {
          title: "决赛",
          list: [
            [
              {
                name: "EDG",
                win: true,
                id: 1,
              },
              {
                name: "DWG",
                win: false,
                id: 2,
              },
            ],
          ],
        },
        {
          title: "冠军",
          list: [
            {
              name: "EDG",
              win: true,
              id: 1,
            },
          ],
        },
      ],
```

### config

```js
{
          initheight: 50, // 对垒单元格高度
          itemHeight: 40, // 单元格高度
          mb: 10, // 相邻对垒单元格距离
          justify: "flex-start", //文本对其 center flex-end flex-start
          borderWidth: 2, // border宽度
          borderColor: "#f05b5b", // 连接线颜色
          win: {
            // 胜利单元格样式
            backgroundColor: "rgb(250, 224, 224)",
            color: "#f05b5b",
            borderColor: "#f05b5b",
          },
          lose: {
            // 失败单元格样式
            backgroundColor: "#f2f2f2",
            color: "rgba(0, 0, 0, 0.65)",
            borderColor: "#ccc",
          },
        };
```

## 插槽

### header

> 顶部title插槽

```vue
<template v-slot:header>
   <span>顶部插槽</span>
</template>
```

### none

> 暂无数据插槽

```vue
<template v-slot:none>
   <h1>暂无数据</h1>
</template>
```