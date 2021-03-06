Vue + Node + MongoDB 学习笔记
===

> create by **jsliang** on **2018-10-16 21:48:25**  
> Recently revised in **2018-10-16 21:48:29**

<br>

# 第一章 印象

* Vue 是一个灵活的、渐进式框架：声明式渲染 -> 组件系统 -> 客户端路由 -> 大规模状态管理 -> 构建工具  

* Vue 区别于 jQuery：

1. 数据驱动。不同于 jQuery 的命令式操作，不需要大规模对 DOM 节点的更新替换，Vue 更专注于数据层，通过数据层的改变，来渲染页面。  

&emsp;&emsp;View(DOM) <---> ViewModule(Vue) <---> Model(POJO - 原生JS对象)

2. 组件化。在 jQuery 中，一些业务逻辑不能更好的提取出来。而 Vue 可以对一些常用的功能模块进行抽取，形成组件：例如购物车、登录。

* Vue 如何实现双向数据绑定的关键： Object.defineProperty 的 get 和 set 方法。案例可以找： `E:\学习资料\实战\Vue+Node+Mongodb\第1章课程介绍\1.3vue概括核心思想.wmv`

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Vue 双向数据绑定实现</title>
</head>
<body>
    <input type="text" id="userName">
    <br>
    <span id="uName"></span>

    <script>
        var obj = {};
        Object.defineProperty(obj, "userName", {
            get: function() {
                console.log("get init");
            },
            set: function(val) {
                console.log("set init");
                document.getElementById("uName").innerText = val;
                document.getElementById("userName").value = val;
            }
        });
        document.getElementById("userName").addEventListener("keyup", function(event){
            obj.userName = event.target.value;
        })
    </script>
</body>
</html>
```

* 通过 vue-cli 搭建的环境，是 SPA 单页应用。
* 如果需要使用 Vue 搭建多页面应用，需要通过 `<script>` 标签引用 Vue，或者配置 Webpack 来开发 Vue 的多页面应用。

* 通过 vue-cli 构建 SPA 应用：
1. 全局安装 vue-cli ：`npm i vue-cli -g`
2. 简洁生成：`vue init webpack-simple demo` || 完整生成：`vue init webpack demo2`
3. 安装依赖：`cnpm i`

<br>

# 基础语法：

1. 模板语法

* Mustache 语法： {{ msg }}
* HTML 赋值：v-html = ""
* 绑定属性：v-bind:id= ""
* 使用表达式：{{ ok ? 'yes' : 'no' }}
* 文本赋值：v-text = ""
* 指令：v-if = ""
* 过滤器： {{ message || capitalize }} 和 v-bind:id = " rawId | fromatId "

<br>

2. Class 和 Style 绑定

* 对象语法：v-bind:class="{ 'active':isActive, 'text-danger':hasError }"
* 数组语法：

```
<div v-bind:class="{activeClass, errorClass}">
</div>

data: {
    activeClass: 'active',
    errorClass: 'text-danger'
}
```

* style 绑定-对象语法：v-bind:style = "{ color: activeColor, fontSize: fontSize + 'px' }"

<br>

3. 条件渲染

* v-if：`v-if` 判断，如果否，则连 DOM 节点都不产出。
* v-else：相反于 `v-if`。
* v-else-if：`v-if` 的多种判断情况。
* v-show：不同于 `v-if`，该条件渲染产生了 DOM 节点，它只是控制 DOM 的显示隐藏，有则 `display: block`，无则 `display: none`。
* v-cloak：

<br>

4. Vue 事件处理器

* v-on:click = "greet" 或者 @click = "greet"
* v-on:click.stop、v-on:click.stop.prevent、v-on:click.self、v-on:click.once
* v-on:keyup.enter

<br>

5. Vue 组件

* 全局组件和局部组件
* 父子组件通讯-数据传递
* Slot

<br>

> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="知识共享许可协议" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><a xmlns:dct="http://purl.org/dc/terms/" property="dct:title">**jsliang** 的文档库</a> 由 <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/LiangJunrong/document-library" property="cc:attributionName" rel="cc:attributionURL">梁峻荣</a> 采用 <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">知识共享 署名-非商业性使用-相同方式共享 4.0 国际 许可协议</a>进行许可。<br />基于<a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/LiangJunrong/document-library" rel="dct:source">https://github.com/LiangJunrong/document-library</a>上的作品创作。<br />本许可协议授权之外的使用权限可以从 <a xmlns:cc="http://creativecommons.org/ns#" href="https://creativecommons.org/licenses/by-nc-sa/2.5/cn/" rel="cc:morePermissions">https://creativecommons.org/licenses/by-nc-sa/2.5/cn/</a> 处获得。