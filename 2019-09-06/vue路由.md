<h1>vue ·��</h1>


·�ɣ�·�ɱ����Ƕ�Ӧ��ϵ

���·�ɣ����ݲ�ͬ���û�URL���󣬷��ز�ͬ����
���ʣ�URL�����ַ���������Դ֮��Ķ�Ӧ��ϵ

ǰ��·�ɣ����ݲ�ͬ���û��¼�����ʾ��ͬ��ҳ������
���ʣ��û��¼����¼�������֮��Ķ�Ӧ��ϵ

ʵ�ּ��׵�ǰ��·��

����URL��hashʵ��

window.onchange=function(){
   console.log(location.hash)
}

vue Router

vue Router(������http://router.vue.js.org/zh/)��vue�ٷ���·�ɹ�����
��vue.js�ĺ�����ȼ��ɣ����Էǳ����������SPAӦ�ó���Ŀ�����
vue router�����Ĺ����У�

֧��HTML5��ʷģʽ��hashģʽ

֧��Ƕ��·��

֧��·�ɲ���

֧�ֱ��ʽ·��

֧������·��

����ʹ�ò���

1.������ؿ��ļ���������vue.js�ļ���
2.���·�����ӣ�<router-link to="user"></router-link����
3.���·�����λ <router-view></router-view>
4.����·����� const user={}
5.����·�ɹ��򲢴���·��ʵ��
const router=new VueRouter({

  routes:[{

   {path:'/user',component:'user'}
}]
}

})
6.��·�ɹ��ص�vue��ʵ����vmʵ��������



·���ض���

������·�ɹ����м���
{path:'/',redirect:'/user'}

Ƕ��·���÷� 

Ƕ��·������
 ����·��ͨ��children���������Ӽ�·��
  const router=new VueRouter({
    routes:[
      {path:'/user',componet:user},
      {path:'/register',component:Register,
       //ͨ��children���ԣ�Ϊregister�����·�ɹ���
      children:[
      {path:'/register/tab1',component:Tab1},
       {path:'/register/tab2',component:Tab2}
]

}
]

})

��̬ƥ��·��

Ӧ�ó�����ͨ����̬·�ɲ�����ģʽ����·��ƥ��

1.var router=new VueRouter({
   routes:[
   //��̬·������ ��ð�ſ�ͷ
   {path:'/user/:id',component:user}
]
})

conser user={
      //·�������ͨ��$route.parmas ��ȡ·�ɲ���
      tempiate:'<div>user{{$route.parmas.id}}</div>'


}

2.$route���Ӧ·���γɸ߶���ϣ����������Կ���ʹ��props�������·�ɽ���
//props Ϊ��������
var router=new VueRouter({
   routes:[
   //���props������Ϊture,route.parmas���ᱻ����Ϊ�������
   {path:'/user/:id',component:user��props:ture}
]
})

conser user={
       props:['id'], ʹ��props����·�ɲ���
      
      tempiate:'<div>user{{id}}</div>'//ʹ��·�ɲ���


}
//props Ϊ��������
var router=new VueRouter({
   routes:[
   //���props��һ���������ᱻ��ԭ������Ϊ������� 
   {path:'/user/:id',component:user��props:{uname��lisi,age:12 }}
]
})

conser user={
       props:['uname','age'], ʹ��props����·�ɲ���
      
      tempiate:'<div>user{{uname+'---'+age}}</div>'//ʹ��·�ɲ���


}

//props Ϊ��������
var router=new VueRouter({
   routes:[
   //���props��һ���������������������route����Ϊ�Լ����β� 
   {path:'/user/:id',component:user��props:route=>({

          uname:'zs',
          age:20,
          id:route.params.id

})}
]
})

conser user={
       props:['uname','age','id'], ʹ��props����·�ɲ���
      
      tempiate:'<div>user{{uname+'---'+age}}</div>'//ʹ��·�ɲ���


}

����·��
 Ϊ�ָ��ӷ���ı�ʾ·��·�������Ը�·�ɹ�����һ������

const touter=new VueRouter({
    route:[{
           path:'/user/:id',
           name:'user',
           component:user
}]
})
 <router-link :to='{name:'user',parmas:{id:123}}'>user</router-link>
 router.push({name:'user',params:{id:123}})


vue-router��̵���

ҳ�浼�������ַ�ʽ������ʽ���������ʽ����
����ʽ������ͨ���������ʵ�ֵ�����ʽ����������ʽ����
���ʽ������ͨ������javascript��ʽ��APIʵ�ֵ����ķ�ʽ���������ʽ����


���ʽ���������÷�

���ñ��ʽ����API
this.$router.push('hash��ַ')
this.$router.go(n)

����

const user={
  template:`<div><button @click="goRegister">��ת��ע��ҳ��</button></div>`,
  methods:{
           goRegister: function(){
           //�ñ�̷�ʽʵ��ҳ����ת
           this.$router.push('/register');
}
}
}