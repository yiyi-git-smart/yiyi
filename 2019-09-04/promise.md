1.Promis基本用法
 
实例化Promis对象，构造函数中传递函数，该函数中用于处理异步任务

resolve和reject两个参数用于处理成功和失败两种情况，并通过p.then获取处理结果

例：

var p=new Promise(function(resolve,reject){
    
  //成功时调用 resolve()
  //失败时调用 reject()

});
p.then(function(ret){
     // 从resolve得到正确结果}，

       function(ret){
        
       //从reject得到错误信息

},
})；

2.基于Promise处理Ajax请求

1。处理原生Ajax

 function queryData(url){
    var p=new Promise(function(resolve,reject){
        var xhr=new XMLhttpquest();
        xhr.onreadystatechange=function(){
        if(xhr.readyState!=4)return;
        if(xhr.readyState==4&&xhr.status==200){
         resolve(xhr.responseText);
}else{
         reject('服务器出错')

}
}；
         xhr.open('get',url);
         xhr.send(null);
});
         return p;

}
* queryData('http://localhost:3000/data')
    .then(function(data){
     console.log(data);},
     function(info){
     console.log(info);
}

})*

//发送多次Ajax请求

 queryData('http://localhost:3000/data')
    .then(function(data){
     console.log(data);
     return queryData('http://localhost:3000/data1');
})
     .then(function(data){
     console.log(data);
     return queryData('http://localhost:3000/data2');
})
     .then(function(data){
     console.log(data);
});

3.then 参数的函数返回值

1.返回Promise实例对象
返回的对象调用下一个then

2.返回普通值
返回普通值会直接传递给下一个then,通过then参数中函数的参数接收该值


4 Promise 常用API

1.实例方法
p.then() 得到异步任务正确结果
p.catch() 获取异常信息
p.finally()成功与否都会执行（还不是正式标准）

2.对象方法

Promise.all() 并发处理多个异步任务，所有任务都执行完成才能得到结果

Promise.race()并发处理多个异步任务，只有一个任务完成就能得到结果

Promise.all(p1,p2,p3).then((result)=>{
  console.log(result);

})
Promise.all(p1,p2,p3).then((result)=>{
  console.log(result);

})




















