# 页面滚动的几种方式 

[功能预览](https://71mcy.csb.app/#topAnchor)

html 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }
    div{
        background-color:#abf3ae;
        height: 200px;
        margin-bottom: 20px;
    }
</style>
<body>
     <contain class="test1">
        <a name="topAnchor"></a>
        <div id="top">我是顶部</div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div id="middler">我是中间</div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
    </contain>
    <footer>
        <button id="backTop1">第一种方式回到顶部</button>
        <button id="backTop2">第二种方式回到中间</button>
        <button id="backTop3">第三种方式回到顶部</button>
    </footer>
</body>
</html>
```

### 使用 a 标签 锚点动能

```javascript
backTop1.addEventListener("click", function (e) {
    let a = document.createElement("a")
    a.href = "#topAnchor"
    e.target.appendChild(a)
    a.onclick = function (e) {
        e.stopPropagation()
    }
    a.click()
    e.target.removeChild(a)
})
```

### 使用 Element scrollIntoView api

```javascript
const backTop2 = document.getElementById("backTop2")
const c = document.getElementById("middler")
backTop2.addEventListener("click", function (e) {
    c.scrollIntoView({ behavior: "smooth" })
})
```

### 使用 requestAnimationFrame api

```javascript
const distance = 80;// 滚动条每次滚动的距离
function up(){
    let start = document.documentElement.scrollTop;
    function gotop() {
        scrollTo(0, start - distance)
        start = start - distance
        if (start >0 ){
            window.requestAnimationFrame(gotop)
        }
    }
    window.requestAnimationFrame(gotop)
    }
    
const backTop3 = document.getElementById("backTop3")
backTop3.addEventListener("click", function (e) {
    up()
})

```
