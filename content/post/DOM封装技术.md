 # 2020/1/29  <DOM>封装部分笔记内容 
 (html里面有2个js，分别是dom.js和main.js)
 # 增
 ## * 关于创建节点的万能的创建方法
 (dom.create(`<div>hi</div>`)用于创造节点)

 dom.js
```
window.dom = {
    create(string) {
        const container = document.createElement("template");
        container.innerHTML = string.trim();
        return container.content.firstChild;

    }
}
```
 main.js
```
const div = dom.create("   <td>hi</td>");
console.log(div);
```
## *  给一个节点，后面加一个节点怎么做
(dom.after(node,node2))
 dom.js
```
after(node,node2){
    node.parentNode.insertBefore(node2,node.nextSibling);
}
```
 main.js
```
dom.after(我是之前的节点,我是弟弟我是要加在后加的节点);
```
## *  给一个节点，前面加一个节点
(dom.before(node,node2))//下面我也不写了，可以参考第38行
 dom.js
```
before(node,node2){
    node.parentNode.insertBefore(node2,node);
}
```
 main.js
```
dom.before(我是之前的节点,我是弟弟我是后加在前面的节点);
```
//以后关于main.js 我能不写则不写了
## * 如果给节点加给儿子

 dom.js
```
append(parent,node){
    parent.appendChild(node)
}
```
## * 给节点新增一个爸爸
 dom.js
```
wrap(node,parent){
    dom.before(node,parent)
    dom.append(parent,node)
}
```
这个不怎么好理解所以我画了幅画帮助理解
![图片](图片/批注&#32;2020-01-29&#32;225311.png)

# 删
## * 删除节点
```
remove(node){
    node.remove()
}  //这个方法比较新ie可能不支持，
所以我们有老办法

remove(node){
    node.parentNode.removeChild(node)
    return node
}
```
## * 干掉节点的所有儿子
```
empty(node){
    //const childNodes = node.childNodes(可以简写成下面一句)
    const {childNodes} = node
    const array = []
    let x = node.firstChild
    while(x){
        array.push(dom.remove(node.firstChild))
        x = node.firstChild
    }
    return array
}
```
# 改
## * 如何改或者读取一个div的title
main.js
```
dom.attr(test,'title','Hi,I am Sam')//实现了写
const title = dom.attr(test,'title')//实现了读
console.log(`title:${title}`)//返回给一个变量为，再呈现出来
```
dom.js
```
//重载
attr(node,name,value){
    if(arguments.Length === 3){
        node.setAttribute(name,value)
    }else if(arguments.Length === 2){     
        return node.getAttribute(name)
    }
}
```
## * 如何读写(设置)文本内容
main.js
```
dom.text(text,'你好，这是新的内容`)
```
dom.js
```
//适配
text(node,string){
    if(argument.length === 2){
    if(`innerText` in node){
    node.innerText = string
}else{
    node.textContent = string
}
}else if(arguments.length === 1){
    if(`innerText` in node){
    return node.innerText
}else{
    return node.textContent 
}
}

```
## * 如何读写(设置)html
main.js
```
dom.text(text,'你好，这是新的内容')
dom.text(text)
```
dom.js
```
html(node,string){
    if(arguments.length === 2){
        node.innerHTML = string
    }else if(arguments.length ===1){
        return node.innerHTML
    }
}
```
## * dom.style(node,{color:'red'})用于修改style
main.js
```
dom.style(test,{border:'1px solid red',color:'blue'})
dom.style(text,'border')
dom.style(text,'border','1px solid red')
```
dom.js
```
style(node,object){
    if(argument.length===3){
        //dom.style(div,'color','red')
        node.style[name] = value    
    }else if(arguments.length===2){
        if(type of name==='string'){
            //dom.style(div,'color')
            return node.style[name]
        }else if (name instance of object){
            // dom.style(div,{color:'red'})
            for(let key in name){
                node.style[key]=name[key]
            }


        }
    }
    for(let key in object){
        //key:border/color
        //node.style.border = .....
        //node.style.color = .....
        node.style[key] =object[key]
    }
}
```
## * dom.class.add(node,'red')用于添加class
main.js
```
dom.class.add(test,'red')
```
dom.js
```
class:{
    add(node,className){
        node.classList.add(className)
    },
    remove(node,className){
        node.classList.remove(className)
    },
    has(node,className){
       return node.classList.contains(className)
    }
}
```
## * dom.on(node,'click',fn)用于添加事件监听
main.js
```
const fn = ()=>{
    console.log('点击了')
}
dom.on(test,'click',fn)
dom.off(test,'click',fn)
```
dom.js
```
on(node,eventName,fn){
    node.addEventListener(eventName,fn)
},
off(node,eventName,fn){
    node.removeEventListener(eventName,fn)
}
```
# 查
## * dom.find('选择器')用于获取标签或者标签们
dom.js
```
find(selector,scope){
    return (scope //document).querySelectorAll(selector)
}
```
main.js
```
const testDiv = dom.find('#test')[0]
dom.find('.red',testDiv)[0]//在哪里找
console.log(testDiv)

```

## * 找出元素的爸爸
main.js
```
console.log(dom.parent(text))
```
dom.js
```
parent(node){
    return node.parentNode
}
```
## * 找儿子
dom.js
```
children(node){
    return node.children
}
```
## * 找兄弟姐妹
dom.js
```
siblings(node){
    return Array.from(node.parentNode.children).filter(n=>n!===node)
}
```
main.js
```
const s2 = dom.find('#s2')[0]
console,log(dom.siblings(s2))
```
## * 找弟弟
dom.js
```
next(node){
    let x = node.nextSibling
    while(x && x.nodeType === 3){
        x = x.nextSibling
    }
    return x
}
```
## * 找哥哥
dom.js
```
previous(node){
    let x = node.previousSibling
    while(x && x.nodeType === 3){
        x = x.nextSibling
    }
    return x
}
```
main.js
```
const s2 = dom.find('#s2')[0]
console.log(dom.previous(s2))
```
## * 遍历所有节点
main.js
```
const t = dom.find('#travel')[0]
dom.each(dom.children(t),(n)=>dom,style(n,'color','red'))
```
dom.js
```
each(nodeList,fn){
    for(let i=0;i<nodeList.length;i++){fn.call(null,nodeList[i])}
}
```
## * 看看儿子是老几
dom.js
```
index(node){
    const list = dom.children(node.parentNode)
    let i
    for( i = 0;i<list.length;i++){
        if(list[i]===node){
            break
        }
    }
    return i
}
```









