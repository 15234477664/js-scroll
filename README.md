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
