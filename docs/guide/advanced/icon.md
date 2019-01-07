# Icon

If you do not find the desired icon in the [Icon](https://github.com/PanJiaChen/vue-element-admin/tree/master/src/icons/svg) of this project, you can select and generate your own business icon library on [iconfont.cn](http://iconfont.cn/)and use it again. Or other svg icon website, download svg and put it in this folder.

## Generate icon library code

First, search for and find the icon you need, and collect it into your shopping cart. In the shopping cart, you can add the selected icon to the project \(if not, create a new one\), and the subsequent generated resources/code are It is based on the dimension of the project.

> If you already have a design draft, just need to generate the relevant code, you can upload your icon, and then do the above operation.

![&#x8D26;&#x6237;&#x76F8;&#x5173;&#x5E03;&#x5C40;](https://gw.alipayobjects.com/zos/rmsportal/jJQYzRyqVFBBamUOppXH.png)

 **This project now supports and recommends separate export of svg usage. Download method as shown below:**

![](https://wpimg.wallstcn.com/1f8b1e56-cfd9-4ef7-a0aa-dfb0c2883aa3.gif)

After the download is complete, the downloaded .svg file is automatically imported after it is placed in the `@/icons/svg` folder.

## How to use

```javascript
<svg-icon icon-class="password" /> //Icon-class is the icon's name usage
```

[Component](https://github.com/forwardfirst/vue-element-admin-site/tree/4baf3651fa649e12721a152722f6e90c13a20772/component/svg-icon.md)

## Change color

`svg-icon` reads its parent's color \`fill: currentColor;' by default.

You can change the parent's `color` or change the color of `fill` directly.

:::tip If you encounter an incorrect icon color, you can refer to this[issue](https://github.com/PanJiaChen/vue-element-admin/issues/330) :::

## Detailed articles

[手摸手，带你优雅的使用 icon](https://juejin.im/post/59bb864b5188257e7a427c09)

