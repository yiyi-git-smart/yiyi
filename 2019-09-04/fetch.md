fetch
1.基本特性

 更加简单的数据获取方式，功能更强大、更灵活，可以看作xhr的升级版
 基于Promise实现

2.语法结构
  fetch(url).then(fn2)
            .then(fn3)
            ....
            .catch(fn)

http://developer.mozilla.org/en-US/docs/Web/API/Fetch_API(fetch API使用说明)

3.基本用法

fetch('http://localhost:3000/fdata').then(data=>{
return data.text();//text()方法属于fetch, 得到的是Promise实例对象,用于获取后台的数据
}).then(ret=>{

//注意这里才得到最终数据

console.log(ret);

})

4 fetch 接口调用方法 
fetch 请求参数 
get 方式去请求参数

1.fetch('/abc?id=123',{
method: 'get'

}).then(data=>{
return data.text();//text()方法属于fetch, 得到的是Promise实例对象,用于获取后台的数据
}).then(ret=>{

//注意这里才得到最终数据

console.log(ret);

})

2.fetch('/abc/123',{
method: 'get'

}).then(data=>{
return data.text();//text()方法属于fetch, 得到的是Promise实例对象,用于获取后台的数据
}).then(ret=>{

//注意这里才得到最终数据

console.log(ret);

})

DELETE方式请求参数 
.fetch('/abc/123',{
method: 'delete'

}).then(data=>{
return data.text();//text()方法属于fetch, 得到的是Promise实例对象,用于获取后台的数据
}).then(ret=>{

//注意这里才得到最终数据

console.log(ret);

})
POST请求方式的参数传递

fetch('/abc/123',{
method: 'post',
body:'uname=lisi&pwd=123',
headers:{

   'Content-Yype':'application/x-www-form-urlencoded',//必须有

}

}).then(data=>{
return data.text();//text()方法属于fetch, 得到的是Promise实例对象,用于获取后台的数据
}).then(ret=>{

//注意这里才得到最终数据

console.log(ret);

})

fetch('/abc/123',{
method: 'post',
body:JSON.strinhify({
 uname:'张三'，
 pwd:12,
}),
headers:{

   'Content-Yype':'application/json',//必须有

}

}).then(data=>{
return data.text();//text()方法属于fetch, 得到的是Promise实例对象,用于获取后台的数据
}).then(ret=>{

//注意这里才得到最终数据

console.log(ret);

})
后台接口
// POST请求参数张三12 
app.post('/abc/123',(req,res)=>{
res.send('POST请求参数！'+req.body.uname+req.body.pwd)

})

put 请求参数

fetch('/abc/123',{
method: 'put',
body:JSON.strinhify({
 uname:'张三'，
 pwd:12,
}),
headers:{

   'Content-Yype':'application/json',//必须有

}

}).then(data=>{
return data.text();//text()方法属于fetch, 得到的是Promise实例对象,用于获取后台的数据
}).then(ret=>{

//注意这里才得到最终数据

console.log(ret);

})
后台接口
// POST请求参数张三12 
app.post('/abc/123',(req,res)=>{
res.send('POST请求参数！'+req.body.uname+req.body.pwd)

})