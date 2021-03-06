# FrontEnd Key Point
## HTML

### Web语义化与SEO

Web语义化是指使用语义恰当的标签，使页面**有良好的结构**，页面元素**有含义**，能够让**开发者**和**搜索引擎**都容易理解。另外带有语义的标签也更易于被其它设备（屏幕阅读器，盲人阅读设备和移动设备）解析。

*那么搜索引擎的爬取页面的时候，有哪些需要注意的点呢？*
> 1. 优化网页标题，关键字和内容描述等
> ```
>  <title>网易</title>
>  <meta name="Keywords" content="网易,邮箱,游戏,新闻,体育,娱乐,女性,亚运,论坛,短信,数码,汽车,手机,财经,科技,相册">
>  <meta name="Description" content="网易是中国领先的互联网技术公司，为用户提供免费邮箱、游戏、搜索引擎服务，开设新闻、娱乐、体育等30多个内容频道，及博客、视频、论坛等互动交流，网聚人的力量。">
> ```
>
> 2. 使用带有语义的标签
> 标题：h1,h2,h3......
> 内容：section, article, aside, header, footer, nav, figure, figcaption, time, mark & main
> 

### 浏览器工作原理

从在地址栏输入URL后，发生的事情讲起：

1. DNS查询，获取目标服务器的IP地址；
2. 建立HTTP/HTTPS链接，获取服务端返回的数据（HTML字符串的字节流）；
3. 解析渲染页面：
    1. 解析HTML Tag，生成DOM树（**构建阶段**）；
    2. 在解析HTML Tag时，如果碰到CSS样式相关代码，则解析CSS代码，生成CSSOM（**构建阶段**：）；
    3. 在碰到script标签时，停止对DOM树的构建，解析脚本（**构建阶段**：）；
    4. 将解析出来的CSSOM 附加到DOM上，生成渲染树(**Render Tree**），渲染树不包括元素的位置和大小信息；
    5. 对DOM元素进行布局，计算元素的位置和大小信息（**Layout Tree**）；
    6. 渲染DOM树到显示屏（**Painting**）；

PS： 为了尽快将页面呈现给用户，浏览器不会等到所有的HTML都加载完毕再渲染，而是会尽快地解析。


#### 布局相关 position 和 float

定位方案：
1. 普通定位，根据元素在Render Tree中的位置依次进行位置计算，跟元素则DOM树中的位置一致或者接近；
2. 浮动定位，对象先按照普通流进行布局，然后尽可能地向左或向右移动；
3. 绝对定位，对象在呈现树中的位置和它在 DOM 树中的位置不同；

#### extra:
> 在解析HTML生成DOM过程中，需要用到**解析算法**（[HTML5 规范详细地描述了解析算法](http://www.whatwg.org/specs/web-apps/current-work/multipage/parsing.html)）。
>  因为 HTML 无法用常规的自上而下或自下而上的解析器进行解析。原因在于：
>  1. 语言的宽容本质。
>  2. 浏览器历来对一些常见的无效 HTML 用法采取包容态度。
>  3. 解析过程需要不断地反复。源内容在解析过程中通常不会改变，但是在 HTML 中，脚本标记如果包含 document.write，就会添加额外的标记，这样解析过程实际上就更改了输入内容。
>  


#### CSS解析

CSS规则集？
CSS层叠顺序？



