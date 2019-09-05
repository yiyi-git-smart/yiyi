axios�ӿڵ��� 

axios(������http://github.com/axios/axios)��һ������Promise�����������node.js��HTTP�ͻ��ˡ�

��������

֧���������node.js

֧��Promise

�������������Ӧ

�Զ�ת��JSON���� 

�����÷�
 
 axios.get('/abc').then(function(ret){
   console.log(ret.data)
 //data�����ǹ̶��÷� ��ȡ��̨ʵ������

})
  ��˽ӿ���ʽ
  app.get('/abc',(req,res)=>{

     res.send('hello axios')

})

axios ����API

get: ��ѯ����

post:�������

put: �޸�����

delete: ɾ������

1.GET��ʽ���в������� 

ͨ��url����

 axios.get('/abc��id=123').then(function(ret){
   console.log(ret.data)

})
  ��˽ӿ���ʽ
  app.get('/abc',(req,res)=>{

     res.send('axiosͨ��get��ʽ���ݲ���'+req.query.id)

})

 axios.get('/abc/123').then(function(ret){
   console.log(ret.data)

})
  ��˽ӿ���ʽ
  app.get('/abc/��id',(req,res)=>{

     res.send('axiosͨ��get(Restful)��ʽ���ݲ���'+req.params.id)

})

ͨ��params ѡ��ݲ���

 axios.get('/abc',{
  params:{
   id:789,

}

}).then(function(ret){
   console.log(ret.data)

})
 ��˽ӿ���ʽ
  app.get('/abc',(req,res)=>{

     res.send('axiosͨ��get��ʽ���ݲ���'+req.query.id)

})

DELETE��ʽ���ݲ��� ��GET���ݲ�������

����
 axios.delete('/abc��id=123').then(function(ret){
   console.log(ret.data)

})
  ��˽ӿ���ʽ
  app.delete('/abc',(req,res)=>{

     res.send('axiosͨ��get��ʽ���ݲ���'+req.query.id)

})

POST ���ݲ�����Ĭ�ϵ���json���ݣ�

1.axios.post('/abc',{
   uname:'lisi',

   pwd:123


}).then(function(ret){
   console.log(ret.data)

})
 ��˽ӿ���ʽ
  app.post('/abc',(req,res)=>{

     res.send('axiosͨ��post��ʽ���ݲ���'+req.body.uname+'--'+req.body.pwd)

})

2.ͨ��URLSearchParams���ݲ�����application/xwwwformurlencoded��
  const params=new URLSearchParams();
  parmas.apppend('param1','value1');
  params.append('parmas2','value2');
   axios.post('/abc',parmas).then(function(ret){
   console.log(ret.data)

})

put ���ݲ�����post����


axios.put('/abc',{
   uname:'lisi',

   pwd:123


}).then(function(ret){
   console.log(ret.data)

})
 ��˽ӿ���ʽ
  app.post('/abc/��id ',(req,res)=>{

     res.send('axiosͨ��put��ʽ���ݲ�����+req.parmas.id+'---'+req.body.uname+'--'+req.body.pwd)

})

axios ����Ӧ���(����)
 
 data:ʵ����Ӧ���������ݣ�json���ݣ�
 hearders:��Ӧͷ��Ϣ
 status:��Ӧ״̬��
 statusText:��Ӧ״̬��Ϣ

axiosȫ������

axios.defaults.timeout=3000;//��ʱʱ��
axios.default.baseURL ='URL��ַ'//��������Ļ�׼��ַ
����
axios.defaults.baseURL ='http://localhost:3000/'
 axios.get('/abc').then(function(ret){
   console.log(ret.data)
})//url:http://localhost:3000/abc

axios.defaults.headers['mytoken']='hello'//��������ͷ
 
axios ������
1.�������أ������󷢳�֮ǰ����һЩ��Ϣ

//���һ������������

axios.interceptors.request.use(function(config){
  
//�����󷢳�֮ǰ����һЩ��Ϣ����

return config;
},function(err){

  // ������Ӧ�Ĵ�����Ϣ

})

2.��Ӧ����:�ڻ�ȡ����֮ǰ

axios.interceptors.response.use(function(res){
  
//������Է��ص����ݽ��д���
return res;
},function(err){

  // ������Ӧ�Ĵ�����Ϣ

})

�ӿڵ��� -async/await�÷�
async/await ��ES7 ��������﷨�����Ը��ӷ���Ľ����첽���� 
async �ؼ������ں����ϣ�async �����ķ���ֵ��Promiseʵ������
await�ؼ�������async�������У�await���Եõ��첽�����

�����÷� ��������

async function queryData(id){

 const ret=await axios.get('/data');
 return ret;
}
queryData.then(ret=>{
  console.log(ret)
})

����async function queryData(){

    var ret=await axios.get('data');
    return ret.data;
}
queryData().then(function(data){
 console.log(data)
});

�������첽����

async function queryData(id){
  const info=await axios.get('/async1');
  const ret= await axios.get('async?info='+info.data);
  return ret;

}
queryData.then(ret=>{
 console.log(ret)
})

����
async function queryData(id){
  const info=await axios.get('/async1');
  const ret= await axios.get('async2?info='+info.data);
  return ret.data;

}
queryData.then(data=>{
 console.log(data)
})
��˽ӿ���ʽ
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