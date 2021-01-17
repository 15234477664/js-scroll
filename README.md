# js-scroll
实现两个滚动条同步滚动
```html
<div class="leftScroll">
  <div class="tableSon listFourSonTwo">内容描述内容描述内容描述内容描述</div>
  <div class="tableSon listFourSonTwo">内容描述内容描述内容描述内容描述</div>
  <div class="tableSon listFourSonTwo">内容描述内容描述内容描述内容描述</div>
  <div class="tableSon listFourSonTwo">内容描述内容描述内容描述内容描述</div>
</div>
<div class="rightScroll">
  <div class="tableSon listFourSonTwo">内容描述内容描述内容描述内容描述</div>
  <div class="tableSon listFourSonTwo">内容描述内容描述内容描述内容描述</div>
  <div class="tableSon listFourSonTwo">内容描述内容描述内容描述内容描述</div>
  <div class="tableSon listFourSonTwo">内容描述内容描述内容描述内容描述</div>
</div>
```
```js
<script>
    var l =document.querySelector('.leftScroll')
    var r =document.querySelector('.rightScroll')
    var scales = (l.scrollHeight - l.clientHeight) / (r.scrollHeight - r.clientHeight)
    var flag = true
    l.addEventListener('mousewheel',function(){
        flag = false
        l.addEventListener('scroll',function(){
            if (!flag) {
                r.scrollTop = l.scrollTop / scales
            }
        })
    })
    r.addEventListener('mousewheel',function(){
        flag = true
        r.addEventListener('scroll',function(){
            if (flag) {
                l.scrollTop = r.scrollTop * scales
            }
        })
    })
</script>
```
### 注释：
```html
1、scale为滚动条滚动比例（左边可滚动最大高度/右边可滚动最大高度）
2、clientHeight和offsetHeight均可获取元素高度，这里用clientHeight是因为这个属性不包含横向滚动条的高度
3、scrollHeight是left/right里内容的高度，它和(.left/.right div).clientHeight可能会有区别（例如此例子中p标签有margin值上下都为16px），那么clientHeight不会把最上边的margin-top和最下边的margin-bottom计算进去导致比scrollHeight高度少32px, .left/.right div真实占用空间是包含上下margin的。（当然你也可以用其他方法解决这个高度问题）
4、left/right的mouseover事件来开启/停止当前鼠标所在区域的scroll事件，因为同步滚动只能让一边跟随另一边滚动而滚动，否则两边同时滚动同时改变另一边的scroll, 如果两边不一样高就会导致滚动条缓慢逆流的现象，滚动条拉下来它自己又逆流回去。
```
