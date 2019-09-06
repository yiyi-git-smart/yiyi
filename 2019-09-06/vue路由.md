<h1>vue 路由</h1>


路由：路由本质是对应关系

后端路由：根据不同的用户URL请求，返回不同内容
本质：URL请求地址与服务器资源之间的对应关系

前端路由：根据不同的用户事件。显示不同的页面内容
本质：用户事件与事件处理函数之间的对应关系

实现简易的前端路由

基于URL的hash实现

window.onchange=function(){
   console.log(location.hash)
}

vue Router

vue Router(官网：http://router.vue.js.org/zh/)是vue官方的路由管理器
和vue.js的核心深度集成，可以非常方便的用于SPA应用程序的开发。
vue router包含的功能有：

支持HTML5历史模式或hash模式

支持嵌套路由

支持路由参数

支持编程式路由

支持命名路由

基本使用步骤

1.引入相关库文件（先引入vue.js文件）
2.添加路由链接（<router-link to="user"></router-link〉）
3.添加路由填充位 <router-view></router-view>
4.定义路由组件 const user={}
5.配置路由规则并创建路由实例
const router=new VueRouter({

  routes:[{

   {path:'/user',component:'user'}
}]
}

})
6.把路由挂载到vue根实例即vm实例对象中



路由重定向

在配置路由规则中加入
{path:'/',redirect:'/user'}

嵌套路由用法 

嵌套路由配置
 父级路由通过children属性配置子级路由
  const router=new VueRouter({
    routes:[
      {path:'/user',componet:user},
      {path:'/register',component:Register,
       //通过children属性，为register添加子路由规则
      children:[
      {path:'/register/tab1',component:Tab1},
       {path:'/register/tab2',component:Tab2}
]

}
]

})

动态匹配路由

应用场景：通过动态路由参数的模式进行路由匹配

1.var router=new VueRouter({
   routes:[
   //动态路径参数 以冒号开头
   {path:'/user/:id',component:user}
]
})

conser user={
      //路由组件中通过$route.parmas 获取路由参数
      tempiate:'<div>user{{$route.parmas.id}}</div>'


}

2.$route与对应路由形成高度耦合，不够灵活，所以可以使用props将组件和路由解耦
//props 为布尔类型
var router=new VueRouter({
   routes:[
   //如果props被设置为ture,route.parmas将会被设置为组件属性
   {path:'/user/:id',component:user，props:ture}
]
})

conser user={
       props:['id'], 使用props接收路由参数
      
      tempiate:'<div>user{{id}}</div>'//使用路由参数


}
//props 为对象类型
var router=new VueRouter({
   routes:[
   //如果props是一个对象，它会被按原样设置为组件属性 
   {path:'/user/:id',component:user，props:{uname：lisi,age:12 }}
]
})

conser user={
       props:['uname','age'], 使用props接收路由参数
      
      tempiate:'<div>user{{uname+'---'+age}}</div>'//使用路由参数


}

//props 为函数类型
var router=new VueRouter({
   routes:[
   //如果props是一个函数，则这个函数接收route对象为自己的形参 
   {path:'/user/:id',component:user，props:route=>({

          uname:'zs',
          age:20,
          id:route.params.id

})}
]
})

conser user={
       props:['uname','age','id'], 使用props接收路由参数
      
      tempiate:'<div>user{{uname+'---'+age}}</div>'//使用路由参数


}

命名路由
 为乐更加方便的表示路由路径，可以给路由规则起一个别名

const touter=new VueRouter({
    route:[{
           path:'/user/:id',
           name:'user',
           component:user
}]
})
 <router-link :to='{name:'user',parmas:{id:123}}'>user</router-link>
 router.push({name:'user',params:{id:123}})


vue-router编程导航

页面导航的两种方式：声明式导航及编程式导航
声明式导航：通过点击链接实现导航方式，叫做声明式导航
编程式导航；通过调用javascript形式的API实现导航的方式，叫做编程式导航


编程式导航基本用法

常用编程式导航API
this.$router.push('hash地址')
this.$router.go(n)

例：

const user={
  template:`<div><button @click="goRegister">跳转到注册页面</button></div>`,
  methods:{
           goRegister: function(){
           //用编程方式实现页面跳转
           this.$router.push('/register');
}
}
}