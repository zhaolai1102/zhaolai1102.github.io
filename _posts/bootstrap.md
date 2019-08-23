---
  layout:     post                  #不要管他
  title:      从零开始学Bootstrap     #标题
  subtitle:   bootstrap              #别名,简介,标题下面的那一行字
  date:       2019-08-23            #发表时间
  author:     Zhaolai                    #作者
  header-img: img/post-bg-rwd.jpg   #背景图片
  catalog: true                     #导航目录,不要管他
  original: true                    #是否原创申明
  tags:                             #标签,可以有多个
      - bootstrap
      - html
      - css
      - js
      - 前端
  ---



## 		使用bootstrap

```
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
	<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
</head>
<body>
	<script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
	<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
	<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
</body>
</html>
```

使用link标签导入css样式表

使用script标签导入js脚本

## 页面创建

需要一个容器包裹网站的所有内容

`<div class="container">`

1. container

   用于固定宽度并支持响应式布局的容器。

2. container-fluid

   用于 100% 宽度，占据全部视口（viewport）的容器。

## 网格系统

基于一个12列的布局,响应式的,列会根据屏幕大小自动重新排列

### 网格类别

1. col- 针对所有设备

2. col-sm- 平板 - 屏幕宽度等于或大于 576px
3. col-md- 桌面显示器 - 屏幕宽度等于或大于 768px
4. col-lg- 大桌面显示器 - 屏幕宽度等于或大于 992px
5. col-xl- 超大桌面显示器 - 屏幕宽度等于或大于 1200px

### 网格规则

1. 网格每一行需要放在设置了 .container (固定宽度) 或 .container-fluid (全屏宽度) 类的容器中，这样就可以自动设置一些外边距与内边距。
2. 使用行来创建水平的列组。
3. 内容需要放置在列中，并且只有列可以是行的直接子节点。
4. 预定义的类如 .row 和 .col-sm-4 可用于快速制作网格布局。
5. 列通过填充创建列内容之间的间隙。 这个间隙是通过 .rows 类上的负边距设置第一行和最后一列的偏移。
6. 网格列是通过跨越指定的 12 个可用列来创建。 例如，设置三个相等的列，需要使用用三个.col-sm-4 来设置。
7. Bootstrap 3 和 Bootstrap 4 最大的区别在于 Bootstrap 4 现在使用 flexbox（弹性盒子） 而不是浮动。
8. Flexbox 的一大优势是，没有指定宽度的网格列将自动设置为等宽与等高列 。 如果您想了解有关Flexbox的更多信息，可以阅读我们的CSS Flexbox教程。

### 自动创建等宽列

不指定数字就会根据数量自动平分

```
<div class="container-fluid" style="background-color:red;">
  <h1>Hello World!</h1>
  <div class="row">
    <div class="col" style="background-color:lavender;">.col</div>
    <div class="col" style="background-color:orange;">.col</div>
    <div class="col" style="background-color:lavender;">.col</div>
    <div class="col" style="background-color:orange;">.col</div>
  </div>
</div>
```

### 响应列

如果屏幕小到一定程度就会变成一列

```
<div class="container-fluid">
  <div class="row">
    <div class="col-sm-3" style="background-color:lavender;">.col-sm-3</div>
    <div class="col-sm-3" style="background-color:lavenderblush;">.col-sm-3</div>
    <div class="col-sm-3" style="background-color:lavender;">.col-sm-3</div>
    <div class="col-sm-3" style="background-color:lavenderblush;">.col-sm-3</div>
  </div>
</div>
```

### 不等宽

一行为12列,如果超出那么会被放到第二行,不要大于12

```
<div class="container-fluid">
  <div class="row">
    <div class="col-sm-2" style="background-color:lavender;">.col-sm-3</div>
    <div class="col-sm-3" style="background-color:lavenderblush;">.col-sm-3</div>
    <div class="col-sm-4" style="background-color:lavender;">.col-sm-3</div>
    <div class="col-sm-9" style="background-color:lavenderblush;">.col-sm-3</div>
  </div>
</div>
```

### 自动调整

根据当前分辨率的不同进行调整

```
 <div class="container-fluid">
    <div class="row">
      <div class="col-sm-3 col-md-6 col-lg-4 col-xl-2 bg-success">col-1</div>
      <div class="col-sm-9 col-md-6 col-lg-8 col-xl-10 bg-warning">col-2</div>
    </div>
  </div>
```

### 偏移列

根据 offset-md-X 右移X个格

```
  <div class="container-fluid">
    <div class="row">
      <div class="col-md-4 bg-success">.col-md-4</div>
      <div class="col-md-4 offset-md-4 bg-warning">.col-md-4 .offset-md-4</div>
    </div>
    <div class="row">
      <div class="col-md-3 offset-md-3 bg-success">.col-md-3 .offset-md-3</div>
      <div class="col-md-3 offset-md-3 bg-warning">.col-md-3 .offset-md-3</div>
    </div>
    <div class="row">
      <div class="col-md-6 offset-md-3 bg-success">.col-md-6 .offset-md-3</div>
    </div>
  </div> 
```

## 排版

### 默认设置

1. Bootstrap4 默认的 font-size 为 16px, line-height 为 1.5。

2. 默认的 font-family 为 "Helvetica Neue", Helvetica, Arial, sans-serif。

3. 此外，所有的 **<p>** 元素 margin-top: 0 、 margin-bottom: 1rem (16px)。

4. ```
   <p class="text-muted">柔和的文本。</p>
     <p class="text-primary">重要的文本。</p> 						蓝色
     <p class="text-success">执行成功的文本。</p>					绿色
     <p class="text-info">代表一些提示信息的文本。</p>			浅蓝色
     <p class="text-warning">警告文本。</p>								黄色
     <p class="text-danger">危险操作文本。</p>						红色
     <p class="text-secondary">副标题。</p>							
     <p class="text-dark">深灰色文字。</p>
     <p class="text-light">浅灰色文本（白色背景上看不清楚）。</p>
     <p class="text-white">白色文本（白色背景上看不清楚）。</p>
   ```

5. h1~h6的大小依次为40px,32px,28px,24px,20px,16px,其中16px=1rem

6. 还有更大的 `<h1 class="display-1">`到 `<h1 class="display-4">`,其中1最大

7. `<h1><small></small></h1>`用于写一些相对小和细的文字

8. `<p><mark></mark></p>`拥有黄色背景和内边距

9. `<p><abbr></abbr></p>`拥有虚线下划线

10. `<blockquote class="blockquote">`用于引用的内容`<footer class="blockquote-footer"></footer>`用于引用的位置

11. 描述列表

    ```
      <dl>
        <dt>Coffee</dt>
        <dd>- black hot drink</dd>
    </dl>
    ```

12. 计算机代码`<p><code></code></p>`

13. 键盘输入的内容`<kbd></kbd>`

14. 格式化文本`<pre></pre>`

### 其他

| **类名**            | **描述**                                                     |
| ------------------- | ------------------------------------------------------------ |
| .font-weight-bold   | 加粗文本                                                     |
| .font-weight-normal | 普通文本                                                     |
| .font-weight-light  | 更细的文本                                                   |
| .font-italic        | 斜体文本                                                     |
| .lead               | 让段落更突出                                                 |
| .small              | 指定更小文本 (为父元素的 85% )                               |
| .text-left          | 左对齐                                                       |
| .text-center        | 居中                                                         |
| .text-right         | 右对齐                                                       |
| .text-justify       | 设定文本对齐,段落中超出屏幕部分文字自动换行                  |
| .text-nowrap        | 段落中超出屏幕部分不换行                                     |
| .text-lowercase     | 设定文本小写                                                 |
| .text-uppercase     | 设定文本大写                                                 |
| .text-capitalize    | 设定单词首字母大写                                           |
| .initialism         | 显示在 <abbr> 元素中的文本以小号字体展示，且可以将小写字母转换为大写字母 |
| .list-unstyled      | 移除默认的列表样式，列表项中左对齐 ( <ul> 和 <ol> 中)。 这个类仅适用于直接子列表项 (如果需要移除嵌套的列表项，你需要在嵌套的列表中使用该样式) |
| .list-inline        | 将所有列表项放置同一行                                       |
| .pre-scrollable     | 使 <pre> 元素可滚动，代码块区域最大高度为340px,一旦超出这个高度,就会在Y轴出现滚动条 |

## 颜色

### 颜色类

用于文本,包括链接等

```
  <p class="text-muted">柔和的文本。</p>
  <p class="text-primary">重要的文本。</p> 						蓝色
  <p class="text-success">执行成功的文本。</p>					绿色
  <p class="text-info">代表一些提示信息的文本。</p>			浅蓝色
  <p class="text-warning">警告文本。</p>								黄色
  <p class="text-danger">危险操作文本。</p>						红色
  <p class="text-secondary">副标题。</p>							
  <p class="text-dark">深灰色文字。</p>
  <p class="text-light">浅灰色文本（白色背景上看不清楚）。</p>
  <p class="text-white">白色文本（白色背景上看不清楚）。</p>
```

### 背景颜色类

背景不会自动改变文本的颜色,需要单独设置

```
  <p class="bg-primary text-white">重要的背景颜色。</p>					蓝色
  <p class="bg-success text-white">执行成功背景颜色。</p>			绿色
  <p class="bg-info text-white">信息提示背景颜色。</p>					浅蓝
  <p class="bg-warning text-white">警告背景颜色</p>						黄色
  <p class="bg-danger text-white">危险背景颜色。</p>						红色
  <p class="bg-secondary text-white">副标题背景颜色。</p>
  <p class="bg-dark text-white">深灰背景颜色。</p>
  <p class="bg-light text-dark">浅灰背景颜色。</p>
```

## 表格

1. `<table class="table">`表格样式: 只有行与行之间的表格线,首行下面的稍微粗一点
2.  `<table class="table table-striped">`表格样式: 偶数行有背景颜色, 中灰色
3.  `<table class="table table-bordered ">`表格样式: 增加列与列之间的表格线
4. `<table class="table table-hover ">`表格样式: 被选中的行会变为中灰色
5. `<table class="table table-dark ">`表格样式: 所有的行背景颜色变为黑色
6. `<tr class="table-active">`单独改变行的颜色,颜色同背景颜色类,active表示被选中行的颜色
7. `<thead class="thead-dark">`改变首行的颜色,dark表示黑色,light表示浅灰色
8. `<table class="table table-sm">`表格样式: 间距变小
9. `<table class="table table-responsive">`响应式表格,如果可视宽度低的时候会创建水平滚动条
   1. `<table class="table table-responsive-sm">`<576px
   2. `<table class="table table-responsive-md">` <768px
   3. `<table class="table table-responsive-lg">` <992px  不具体指明的话就是-lg
   4. `<table class="table table-responsive-xl">` <1200px

## 图片

### 图片形状

1. `<img src="图片地址" class="img-rounded">`圆角
2. `<img src="图片地址" class="img-circle">`椭圆
3. `<img src="图片地址" class="img-thumbnail">`图片缩略图,含有一个边框

### 响应式图片

根据窗口大小自动调整图片大小

`<img src = "图片地址" class="img-fluid">`

## 大屏幕

1. 局部

   `<div class="jumbotron">`

   增加标题大小,添加更多的页边距

2. 全屏

   ```
<body>
	<div class="jumbotron jumbotron-fluid">
		<div class="container">
		</div>
	</div>
</body>
   ```

## 提示框

1. `<div class="alert alert-light">`颜色设定和背景颜色设定单词相同

2. `<a href="#" class="alert-link"></a>`自动调整链接颜色

3. 对div添加alert-dismissable类,添加按钮进行关闭操作

   ```
   <div class="alert alert-light alert-dismissable">
   <button type="button" class="close" data-dismiss="alert">&times;</button>
   ```
   
4. 动画,fade隐藏 show展示  加一起就提供淡出淡入功能

   `<div class="alert alert-success alert-dismissable fade show">`

## 按钮

1. 类型

   可以使用`<a></a>,<button></button>,<input>`

   ```
<a href="#" class="btn" role="button">链接按钮</a>
<button type="button" class="btn">按钮</button>
<input type="button" class="btn" value="输入框按钮">
<input type="submit" class="btn" value="提交按钮">
   ```

2. 背景颜色

   `class="btn btn-link"`链接无背景颜色,只有字体颜色,其他的词和背景颜色一致

3. 只保留边框

   `class="btn btn-outline-dark"`

4. 按钮大小

   `class="btn btn-lg"`大按钮

   `class="btn"`普通按钮

   `class="btn btn-sm"`小按钮

5. 块级按钮

   `class="btn btn-block"`

6. 激活禁用

   激活的意思是颜色为鼠标点上去的颜色

   1. 对于button和input

      激活`class="btn active"`

      禁用`class="btn" disabled`

   2. 对于a标签

      激活`class="btn active"`

      激活`class="btn disabled"`

## 按钮组

1. 基本格式

   `  <div class="btn-group">`,数个按钮连在一起
   
   ```
     <div class="btn-group">
       <button type="button" class="btn btn-primary">Apple</button>
       <button type="button" class="btn btn-primary">Samsung</button>
       <button type="button" class="btn btn-primary">Sony</button>
     </div>
   ```
   
2. 按钮大小

   `  <div class="btn-group btn-group-lg">`大按钮

   `  <div class="btn-group btn-group-sm">`小按钮

   `  <div class="btn-group btn-group-xs">`默认按钮大小和没写没啥区别

3. 垂直按钮组

   `<div class="btn-group-vertical">`

4. 下拉菜单

   `class="btn dropdown-toggle" data-toggle="dropdown"`

   ```
   <button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">name</button>
   <div class="dropdown-menu">
   	<a class="dropdown-item" href="#">name1</a>
   	<button type="botton" class="btn dropdown-item btn-primary">name2</button>
   </div>
   ```

5. 拆分下拉菜单

   按钮和菜单分离

   ```
     <div class="btn-group">
       <button type="button" class="btn btn-primary">Sony</button>
       <button type="button" class="btn btn-primary dropdown-toggle dropdown-toggle-split" data-toggle="dropdown">      创建一个空白按钮用于下拉菜单
         <span class="caret"></span>
       </button>
       <div class="dropdown-menu">
         <a class="dropdown-item" href="#">Tablet</a>
         <a class="dropdown-item" href="#">Smartphone</a>
       </div>
     </div>
   ```

## 徽章

1. 凸显内容,会根据父类的大小变化

   `<span class="badge">New</span>`

2. 颜色,必须设置颜色

   `<span class="badge badge-dark">New</span>`

3. 胶囊形状

   `<span class="badge badge-pill badge-dark">`

4. 可以插入其他元素中,如botton

## 进度条

1. 显示百分比

   ```
   <div class="progress">
   	<div class="progress-bar" style="width:70%">这里可以插入文本,如70%</div>
   </div>
   ```

2. 高度设置

   默认16px,`<div class="progress-bar" style="width:70%; height:20px"></div>`

3. 颜色

   `<div class="progress-bar bg-success" style="width:70%"></div>`

   默认是蓝色success绿色info蓝色warning黄色danger红色	

4. 条纹

   `<div class="progress-bar bg-success progress-bar-striped" style="width:70%"></div>`

   默认蓝色,success绿色,info浅蓝色

5. 条纹动画

   `<div class="progress-bar bg-success progress-bar-striped progress-bar-animated" style="width:70%"></div>`

6. 混合彩色

   一根进度条上有很多段

   ```
   <div class="progress">
   	<div class="progress-bar" style="width:70%">这里可以插入文本,如70%</div>
       <div class="progress-bar" style="width:20%">这里可以插入文本,如70%</div>
   	<div class="progress-bar" style="width:10%">这里可以插入文本,如70%</div>
   </div>
   ```

## 分页

1. 基本结构

   ```
   <ul class="pagination">
       <li class="page-item"><a class="page-link" href="#">0</a></li>
       <li class="page-item"><a class="page-link" href="#">1</a></li>
   </ul>
   ```

2. 高亮,变为蓝色

   `<li class="page-item active">`

3. 不可用的分页链接

   `<li class="page-item disabled">`

4. 大小

   `  <ul class="pagination pagination-lg">`

   lg大sm小

5. a/b/c导航

   ```
   <ul class="breadcrumb">
       <li class="breadcrumb-item"><a class="page-link" href="#">0</a></li>
       <li class="breadcrumb-item"><a class="age-link" href="#">1</a></li>
       <li class="breadcrumb-item active">2</li>          表示激活需要去掉a标签
   </ul>
   ```

## 列表

1. 基本结构

   ```
     <ul class="list-group">
       <li class="list-group-item">First item</li>
       <li class="list-group-item">Second item</li>
       <li class="list-group-item">Third item</li>
     </ul>
   ```

2. 激活

   蓝色背景

   `<li class="list-group-item active">First item</li>`

3. 禁用

   灰色的字

   `<li class="list-group-item disabled">First item</li>`

4. 链接列表

   ```
     <div class="list-group">
       <a href="#" class="list-group-item">First item</a>
       <a href="#" class="list-group-item list-group-item-action">Second item</a>   鼠标悬停变为灰色
       <a href="#" class="list-group-item list-group-item-action">Third item</a>
     </div>
   ```

5. 颜色

   `class="list-group-item list-group-item-success"`

   颜色同背景颜色
## 卡片

1. 基本格式

   可以没有头和脚

   ```
   <div class="card">
       <div class="card-header">头部</div>
       <div class="card-body">内容</div> 
       <div class="card-footer">底部</div>
   </div>
   ```

2. 颜色

   ```
   <div class="card bg-primary text-white">
       <div class="card-body">Primary card</div>
   </div>
   ```

3. 标题,正文,链接

   ```
   <div class="card">
       <div class="card-header">
           <h4 class="card-title">卡片标题</h4> 
       </div>
       <div class="card-body">
           <p class="card-text">卡片内容。</p>
       </div>
       <div class="card-footer">
           <a href="#" class="card-link">卡片链接</a>
       </div>
   </div>
   ```

4. 图片卡片

   其中class="card-img-top"卡片位于上方,"card-img-bottom"卡片位于下方

   ```
   <div class="card" style="400px">
       <img class="card-img-top" src="xxx" alt="img" style="width:100%">
       <div class="card-body">
           <p class="card-text">卡片内容。</p>
       </div>
   </div>
   ```

5. 图片背景

   ```
   <div class="card" style="400px">
       <img class="card-img-top" src="xxx" alt="img" style="width:100%">
       <div class="card-img-overlay">		文字置于卡片上方
           <p class="card-text">卡片内容。</p>
       </div>
   </div>
   ```

## 下拉菜单

1. 基本格式

   ```
   <div class="dropdown">			下拉菜单
       <button type="button" class="btn btn-primary dropdown-toggle" data-toggle="dropdown">
         Dropdown button					下拉按钮名称
       </button>
       <div class="dropdown-menu">			下拉列表
           <a class="dropdown-item" href="#">Link 1</a>
           <a class="dropdown-item" href="#">Link 2</a>
           <a class="dropdown-item" href="#">Link 3</a>
       </div>
   </div>
   ```

2. 分割线

   `<div class="dropdown-divider"></div>`,用于a标签与a标签之间

3. 标题

   `<h5 class="dropdown-header">Dropdown header</h5>`不可以点击

4. 高亮

   `<a class="dropdown-item active" href="#">Link 3</a>`

5. 禁用

   `<a class="dropdown-item disabled" href="#">Link 3</a>`

6. 右对齐

   `<div class="dropdown-menu dropdown-menu-right">`下拉列表

7. 向上弹出

   下拉菜单改为`  <div class="dropup">`

## 折叠版

1. 基本格式

   data-target="对应折叠内容的ID值"

   如果是a标签那么使用href可以代替data-target

   ```
   <button type="button" class="btn btn-primary" data-toggle="collapse" data-target="#demo">简单的折叠</button>
   <div id="demo" class="collapse">
   折叠的内容
   </div>
   ```

2. 显示默认内容

   `<div id="demo" class="collapse show">`

3. 手风琴

   使用data-parent将所有折叠元素在指定的父元素下,就可以实现一个选项显示而不是全都关闭和打开

## 导航

1. 基本格式

   ```
   <ul class="nav">
       <li class="nav-item">
           <a class="nav-link" href="#">Link</a>
       </li>
   </ul>
   ```

2. 对齐方式

   1. 默认靠左对齐,指的是导航栏位于容器内的位置
   2. `<ul class="nav justify-content-center">`居中对齐
   3. `<ul class="nav justify-content-end">`靠右对齐

3. 垂直导航

   `<ul class="nav flex-column">`

4. 选项卡

   `<ul class="nav nav-tabs">`

   可以使用`<a class="nav-link active" href="#">Link</a>`标明当前选项卡

   可以使用`<a class="nav-link disabled" href="#">Link</a>`让他无法点击

5. 胶囊导航栏

   `<ul class="nav nav-pills">`激活选项卡时是胶囊状的框

6. 导航等宽

   `<ul class="nav nav-justified">`所有的项目等宽且占满整个容器

7. 下拉菜单

   ```
   <ul class="nav">
       <li class="nav-item dropdown">
           <a class="nav-link dropdown-toggle" data-toggle="dropdown" href="#">Dropdown</a>
           <div class="dropdown-menu">
               <a class="dropdown-item" href="#">Link 1</a>
               <a class="dropdown-item" href="#">Link 2</a>
               <a class="dropdown-item" href="#">Link 3</a>
           </div>
       </li>
   </ul>
   ```

8. 动态选项卡

   ```
   <ul class="nav nav-tabs" role="tablist">    如果想要胶囊式 改为pills
       <li class="nav-item">
           <a class="nav-link active" data-toggle="tab" href="#home">Home</a>    指定href属性到文本,胶囊式tab改为pill
       </li>
       <li class="nav-item">
           <a class="nav-link" data-toggle="tab" href="#menu1">Menu 1</a>    指定href属性到文本,胶囊式tab改为pill
       </li>
   </ul>
   <div class="tab-content">
       <div id="home" class="container tab-pane active"><br>
           <h3>HOME</h3>
           <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
       </div>
       <div id="menu1" class="container tab-pane fade"><br>
           <h3>Menu 1</h3>
           <p>Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
       </div>
   </div>
   ```

## 导航栏

商标,导航,其他元素的集合

### 基础导航栏(横向的)

```
<nav class="navbar navbar-expand-sm bg-light">
    <ul class="navbar-nav">
        <li class="nav-item">
            <a class="nav-link" href="#">Link 1</a>
        </li>
    </ul>
</nav>
```

1. 垂直导航栏

   `<nav class="navbar bg-light">`

2. 不同颜色导航栏

   `<nav class="navbar navbar-expand-sm bg-light navbar-light">`

3. `<li class="nav-item active">`active是保持激活状态

### 商标

   ```
   <nav class="navbar navbar-expand-sm bg-light">
       <a class="navbar-brand" href="#">Logo</a>       logo链接
       <ul class="navbar-nav">
           <li class="nav-item">
               <a class="nav-link" href="#">Link 1</a>
           </li>
       </ul>
   </nav>
   ```

### 折叠导航栏

   ```
   <nav class="navbar navbar-expand-md bg-dark navbar-dark">
       <a class="navbar-brand" href="#">Navbar</a>
       <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#collapsibleNavbar">
           <span class="navbar-toggler-icon"></span>				创建折叠按钮指向菜单
       </button>
       <div class="collapse navbar-collapse" id="collapsibleNavbar">		菜单
           <ul class="navbar-nav">			列表
               <li class="nav-item">
                   <a class="nav-link" href="#">Link</a>
               </li>
               <li class="nav-item">
                   <a class="nav-link" href="#">Link</a>
               </li>
               <li class="nav-item">
                   <a class="nav-link" href="#">Link</a>
               </li>    
           </ul>
       </div>  
   </nav>
   ```

### 下拉菜单

   ```
   <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
       <ul class="navbar-nav">
           <li class="nav-item dropdown">
               <a class="nav-link dropdown-toggle" href="#" id="navbardrop" data-toggle="dropdown">
               Dropdown link
               </a>
               <div class="dropdown-menu">
                   <a class="dropdown-item" href="#">Link 1</a>
                   <a class="dropdown-item" href="#">Link 2</a>
                   <a class="dropdown-item" href="#">Link 3</a>
               </div>
           </li>
       </ul>
   </nav>
   ```

### 表单与按钮

```
<nav class="navbar navbar-expand-sm bg-dark navbar-dark">
    <form class="form-inline">    横版输入
        <input class="form-control" type="text" placeholder="Search">
        <button class="btn btn-success" type="button">Search</button>
    </form>
</nav>
```

还可以增加文本

```
<nav class="navbar navbar-expand-sm bg-dark navbar-dark">
    <form class="form-inline">
        <div class="input-group">
            <span class="input-group-addon">@</span>     文本
            <input type="text" class="form-control" placeholder="Username">
        </div>    
    </form>
</nav>
```

### 非链接文本

```
<nav class="navbar navbar-expand-sm bg-dark navbar-dark">
    <ul class="navbar-nav">
        <li class="nav-item">
            <a class="nav-link" href="#">Link 1</a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="#">Link 2</a>
        </li>
    </ul>
    <span class="navbar-text">文本 </span>
</nav>
```

### 固定

将导航栏固定到顶部或者底部

`<nav class="navbar navbar-expand-sm bg-dark navbar-dark fixed-top">`顶部

`<nav class="navbar navbar-expand-sm bg-dark navbar-dark fixed-bottom">`底部

## 表单

### 堆叠表单

竖着排列

```
<form>
    <div class="form-group">
        <label for="email">Email:</label>
        <input type="email" class="form-control" id="email" placeholder="Enter email">
    </div>
    <div class="form-group">
        <label for="pwd">Password:</label>
        <input type="password" class="form-control" id="pwd" placeholder="Enter password">
    </div>
    <div class="form-check">
        <label class="form-check-label">
            <input class="form-check-input" type="checkbox"> Remember me
        </label>
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

### 内联表单

横着排列

```
<form class="form-inline">
    <label for="email">Email:</label>
    <input type="email" class="form-control" id="email" placeholder="Enter email">
    <label for="pwd">Password:</label>
    <input type="password" class="form-control" id="pwd" placeholder="Enter password">
    <div class="form-check">
        <label class="form-check-label">
            <input class="form-check-input" type="checkbox"> Remember me
        </label>
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

## 表单控件

### 输入input

text,password...

```
<form>
    <div class="form-group">
        <label for="usr">用户名:</label>
        <input type="text" class="form-control" id="usr">
    </div>
</form>
```

### 文本textarea

```
<form>
    <div class="form-group">
        <label for="comment">评论:</label>
        <textarea class="form-control" rows="5" id="comment"></textarea>
    </div>
</form>
```

### 复选框checkbox

```
<form>
    <div class="form-check">     如果都加上form-check-inline可以让所有的选择一行显示
        <label class="form-check-label">
            <input type="checkbox" class="form-check-input" value="">Option 1
        </label>
    </div>
    <div class="form-check">
        <label class="form-check-label">
            <input type="checkbox" class="form-check-input" value="">Option 2
        </label>
    </div>
    <div class="form-check disabled">
        <label class="form-check-label">
            <input type="checkbox" class="form-check-input" value="" disabled>Option 3   这个disabled导致不可以被选中
        </label>
    </div>
</form>
```

### 单选框radio

```
<form>
    <div class="radio">
        <label><input type="radio" name="optradio">Option 1</label>
    </div>
    <div class="radio">
        <label><input type="radio" name="optradio">Option 2</label>
    </div>
    <div class="radio disabled">
        <label><input type="radio" name="optradio" disabled>Option 3</label>   disabled表示不可以选
    </div>
</form>
```

### 下拉菜单select

```
<form>
    <div class="form-group">
        <label for="sel1">多选下拉菜单:</label>     
        <select multiple class="form-control" id="sel1">     去掉multiple变为单选
            <option>1</option>
            <option>2</option>
            <option>3</option>
            <option>4</option>
        </select>
    </div>
</form>
```

## 轮播

```
<div id="demo" class="carousel slide" data-ride="carousel">
                                  指示符
    <ul class="carousel-indicators">
        <li data-target="#demo" data-slide-to="0" class="active"></li>
        <li data-target="#demo" data-slide-to="1"></li>
        <li data-target="#demo" data-slide-to="2"></li>
    </ul>
                                 轮播图片
    <div class="carousel-inner">
        <div class="carousel-item active">
            <img src="https://atts.w3cschool.cn/attachments/knowledge/201803/24575.png">
            					文字说明
            <div class="carousel-caption">
                <h3>图片描述标题</h3>
                <p>描述文字!</p>
            </div>
        </div>
        <div class="carousel-item">
            <img src="https://atts.w3cschool.cn/attachments/knowledge/201801/31740.png">
        </div>
        <div class="carousel-item">
            <img src="https://atts.w3cschool.cn/attachments/knowledge/201804/30601.png">
        </div>
    </div>
                                左右切换按钮
    <a class="carousel-control-prev" href="#demo" data-slide="prev">
        <span class="carousel-control-prev-icon"></span>
    </a>
    <a class="carousel-control-next" href="#demo" data-slide="next">
        <span class="carousel-control-next-icon"></span>
    </a>
</div>
```

## 模态框

```
		按钮用于打开               指向模态框的id
<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#myModal">打开</button>
            模态框 
<div class="modal fade" id="myModal">
    <div class="modal-dialog modal-sm">                打开的是小模态框,使用lg打开大模态框
        <div class="modal-content">
                                  模态框头部
            <div class="modal-header">
                <h4 class="modal-title">模态框头部</h4>
                <button type="button" class="close" data-dismiss="modal">&times;</button>
            </div>
                                  模态框主体
            <div class="modal-body">
                模态框内容..
            </div>
                                   模态框底部
            <div class="modal-footer">
                <button type="button" class="btn btn-secondary" data-dismiss="modal">关闭</button>
            </div>
        </div>
    </div>
</div>
```

## 提示框

只有当鼠标移动上去的时候才会显示的文本框

`  <a href="#" data-toggle="tooltip" title="提示">提示内容</a>`

`data-placement="top"`将提示框显示在什么位置,top上,bottom下,left左,right右

## 弹出框

点击开启,点击关闭,比提示框的内容多

```
<a href="#" data-toggle="popover" title="弹出标题" data-content="弹出的内容">提示内容</a>
<script>
$(document).ready(function(){
    $('[data-toggle="popover"]').popover();   
});
</script>
```

`data-placement="top"`将提示框显示在什么位置,top上,bottom下,left左,right右

`data-trigger="focus"`可以在弹出框的外面点击以关闭弹出框

`data-trigger="hover"`鼠标移动上去显示,移处后消失

## 多媒体

```
<div class="media border p-3">             媒体
    <img src="https://www.w3cschool.cn/attachments/cover/cover_bootstrap4.jpg" alt="John Doe" class="mr-3 mt-3 rounded-circle" style="width:60px;">
    <div class="media-body">               内容
        <h4>bootstrap4教程</h4>
        <p>Bootstrap4 目前是 Bootstrap 的最新版本，是一套用于 HTML、CSS 和 JS 开发的开源工具集。</p>      
    </div>
</div>
```

如果想要让图片显示在右边,只需要将图片写到media-body下面

img增加属性`class="align-self-start"`图片位于顶部

img增加属性`class="align-self-center"`图片位于中间

img增加属性`class="align-self-end"`图片位于底部

## 滚动监听

https://www.w3cschool.cn/bootstrap4/bootstrap4-6bi72qoq.html

## 其他

### 边框

1. 可以定义边框样式

   ```
   <style>
       .border {
           display: inline-block;
           width: 70px;
           height: 70px;
           margin: 6px;
       }
   </style>
   ```

2. 边框颜色 border-dark同背景

3. rounded圆角-top -right -bottom -left -circle椭圆 -0无

### 浮动

1. 浮动class="float-left"左浮动

2. 响应式浮动`<div class="float-sm-right">`
### 其他
1. 居中对齐`class = "mx-auto"`
2. 宽度`w-100` ==> 100%
3. 高度`h-100` ==> 100%