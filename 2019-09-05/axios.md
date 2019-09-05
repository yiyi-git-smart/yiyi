axios接口调用 

axios(官网：http://github.com/axios/axios)是一个基于Promise用于浏览器和node.js的HTTP客户端。

基本特性

支持浏览器和node.js

支持Promise

能拦截请求和响应

自动转换JSON数据 

基本用法
 
 axios.get('/abc').then(function(ret){
   console.log(ret.data)
 //data属性是固定用法 获取后台实际数据

})
  后端接口形式
  app.get('/abc',(req,res)=>{

     res.send('hello axios')

})

axios 常用API

get: 查询数据

post:添加数据

put: 修改数据

delete: 删除数据

1.GET方式进行参数传递 

通过url传递

 axios.get('/abc？id=123').then(function(ret){
   console.log(ret.data)

})
  后端接口形式
  app.get('/abc',(req,res)=>{

     res.send('axios通过get方式传递参数'+req.query.id)

})

 axios.get('/abc/123').then(function(ret){
   console.log(ret.data)

})
  后端接口形式
  app.get('/abc/：id',(req,res)=>{

     res.send('axios通过get(Restful)方式传递参数'+req.params.id)

})

通过params 选项传递参数

 axios.get('/abc',{
  params:{
   id:789,

}

}).then(function(ret){
   console.log(ret.data)

})
 后端接口形式
  app.get('/abc',(req,res)=>{

     res.send('axios通过get方式传递参数'+req.query.id)

})

DELETE方式传递参数 与GET传递参数类似

例：
 axios.delete('/abc？id=123').then(function(ret){
   console.log(ret.data)

})
  后端接口形式
  app.delete('/abc',(req,res)=>{

     res.send('axios通过get方式传递参数'+req.query.id)

})

POST 传递参数（默认的是json数据）

1.axios.post('/abc',{
   uname:'lisi',

   pwd:123


}).then(function(ret){
   console.log(ret.data)

})
 后端接口形式
  app.post('/abc',(req,res)=>{

     res.send('axios通过post方式传递参数'+req.body.uname+'--'+req.body.pwd)

})

2.通过URLSearchParams传递参数（application/xwwwformurlencoded）
  const params=new URLSearchParams();
  parmas.apppend('param1','value1');
  params.append('parmas2','value2');
   axios.post('/abc',parmas).then(function(ret){
   console.log(ret.data)

})

put 传递参数与post类似


axios.put('/abc',{
   uname:'lisi',

   pwd:123


}).then(function(ret){
   console.log(ret.data)

})
 后端接口形式
  app.post('/abc/：id ',(req,res)=>{

     res.send('axios通过put方式传递参数’+req.parmas.id+'---'+req.body.uname+'--'+req.body.pwd)

})

axios 的响应结果(对象)
 
 data:实际响应回来的数据（json数据）
 hearders:响应头信息
 status:响应状态码
 statusText:响应状态信息

axios全局配置

axios.defaults.timeout=3000;//超时时间
axios.default.baseURL ='URL地址'//配置请求的基准地址
例：
axios.defaults.baseURL ='http://localhost:3000/'
 axios.get('/abc').then(function(ret){
   console.log(ret.data)
})//url:http://localhost:3000/abc

axios.defaults.headers['mytoken']='hello'//配置请求头
 
axios 拦截器
1.请求拦截：在请求发出之前设置一些信息

//添加一个请求拦截器

axios.interceptors.request.use(function(config){
  
//在请求发出之前进行一些信息设置

return config;
},function(err){

  // 处理响应的错误信息

})

2.响应拦截:在获取数据之前

axios.interceptors.response.use(function(res){
  
//在这里对返回的数据进行处理
return res;
},function(err){

  // 处理响应的错误信息

})

接口调用 -async/await用法
async/await 是ES7 引入的新语法，可以更加方便的进行异步操作 
async 关键字用于函数上（async 函数的返回值是Promise实例对象）
await关键字用于async函数当中（await可以得到异步结果）

基本用法 （单个）

async function queryData(id){

 const ret=await axios.get('/data');
 return ret;
}
queryData.then(ret=>{
  console.log(ret)
})

例：async function queryData(){

    var ret=await axios.get('data');
    return ret.data;
}
queryData().then(function(data){
 console.log(data)
});

处理多个异步请求

async function queryData(id){
  const info=await axios.get('/async1');
  const ret= await axios.get('async?info='+info.data);
  return ret;

}
queryData.then(ret=>{
 console.log(ret)
})

例：
async function queryData(id){
  const info=await axios.get('/async1');
  const ret= await axios.get('async2?info='+info.data);
  return ret.data;

}
queryData.then(data=>{
 console.log(data)
})
后端接口形式
  app.post('/async1',(req,res)=>{

     res.send('hello')

})
app.post('/async2',(req,res)=>{

     if(req.query.info=='hello'){
        res.send('word')
}else{
    res.send('error')

}
})