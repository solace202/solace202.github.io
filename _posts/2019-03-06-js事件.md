## JavaScript事件

### 事件绑定

* ele.onxxx = function(event) {}，兼容性好，基本等同于写在Html行间上

* obj.addEventListener('on'+type, fn, false);  IE9向下不兼容，可以作为一个事件绑定多个处理程序

* obj.attachEvent('on'+type, fn);  IE独有，一个事件同样可以绑定多个处理程序

### 事件冒泡、捕获

事件冒泡：结构上（非视觉上）嵌套关系的元素，会存在事件冒泡的功能，即同一事件，自子元素冒向父元素。（自底向上）

事件捕获（只有Chrome实现了）：结构上（非视觉上）嵌套关系的元素，会存在事件捕获的功能，即同一事件，自父元素捕获至子元素（事件源元素）。（自顶向上）

触发顺序：先捕获，后冒泡（一个对象的一个事件类型只能遵循一种事件模型）

focus、blur、change、submit、reset、select等事件不冒泡

`obj.addEventListener('on'+type, fn, false);`  绑定事件的最后一个参数false即为事件冒泡，true时即为事件捕获

### 事件委托

event对象中有个属性event.srcElement和event.target来获取事件源对象，在发生事件冒泡时，点击不同区域它的事件源对象其实是不同的。使用场景：

```javascript
// 给每个<li>绑定一个点击事件来获取点击的<li>的内容
<ul>
    <li>1</li>
    <li>2</li>
    .... 中间省略一万个li ...
    <li>9998</li>
    <li>9999</li>
    <li>10000</li>
</ul>
<script>
    // 将点击事件绑定到父元素<ul>中，当点击<ul>时，其实际点击的是<ul>中的<li>
    // 即点击事件的事件源是<li>,就可以获取到<li>的内容了
    var ul = document.getElementByTagName('ul')[0];
    ul.onclick = function(e) {
        var event = e || window.event;
        var target = event.target || event.srcElement;
        console.log(target.innerText);
    }
</script>
```