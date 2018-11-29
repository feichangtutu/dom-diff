## 生成项目
```
npm install -g create-react-app
create-react-app dom-diff
```

## 虚拟dom
createElement => {type,props,children}

## note
### 重绘和回流
> 回流与重绘总结：<br/>
  当render tree中的一部分(或全部)因为元素的规模尺寸，布局，隐藏等改变而需要重新构建。这就称为回流(reflow)。
  每个页面至少需要一次回流，就是在页面第一次加载的时候。在回流的时候，浏览器会使渲染树中受到影响的部分失效，
  并重新构造这部分渲染树，完成回流后，浏览器会重新绘制受影响的部分到屏幕中，该过程成为重绘。<br/>
  当render tree中的一些元素需要更新属性，而这些属性只是影响元素的外观，风格，而不会影响布局的，比如background-color。则就叫称为repaint重绘。 
  注意：回流必将引起重绘，而重绘不一定会引起回流。
  
### dom diff作用
> dom diff是通过js层面的计算，返回一个patch对象，即补丁对象，再通过特定的操作解析patch对象，完成页面的重新渲染

  DOM Diff比较两个虚拟DOM区别 比较两个对象的区别 <br/>
  dom diff作用 根据两个虚拟对象创建出补丁，描述改变的内容，将这个补丁用来更新dom
 
### dom diff三种优化策略
+ 更新时只比较平级
+ 不会跨级对比
+ 同级变化可以复用

### 差异计算

*先序深度优先遍历*

1. 用Javascript对象模拟DOM
2. 把此虚拟dom转为真实dom,并插入到页面中
3. 如果有事件发生修改了虚拟dom,比较两颗虚拟dom树的差异，得到差异对象
4. 把差异对象应用到真正的dom树上

### 计算规则
1. 当节点类型相同时，看属性是否相同，产生一个属性的补丁包 `{type:'ATTRS',attrs:{class:'list-group'}}`
2. 新的dom节点不存在，`{type:'Remove',index:xx}`
3. 节点类型不相同，直接采取替换模式 `{type:'REPLACE',newNode:newNode}`
4. 文本的变化 `{type:'TEXT',text:1}`



 