1.Promis�����÷�
 
ʵ����Promis���󣬹��캯���д��ݺ������ú��������ڴ����첽����

resolve��reject�����������ڴ���ɹ���ʧ�������������ͨ��p.then��ȡ������

����

var p=new Promise(function(resolve,reject){
    
  //�ɹ�ʱ���� resolve()
  //ʧ��ʱ���� reject()

});
p.then(function(ret){
     // ��resolve�õ���ȷ���}��

       function(ret){
        
       //��reject�õ�������Ϣ

},
})��

2.����Promise����Ajax����

1������ԭ��Ajax

 function queryData(url){
    var p=new Promise(function(resolve,reject){
        var xhr=new XMLhttpquest();
        xhr.onreadystatechange=function(){
        if(xhr.readyState!=4)return;
        if(xhr.readyState==4&&xhr.status==200){
         resolve(xhr.responseText);
}else{
         reject('����������')

}
}��
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

//���Ͷ��Ajax����

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

3.then �����ĺ�������ֵ

1.����Promiseʵ������
���صĶ��������һ��then

2.������ֵͨ
������ֵͨ��ֱ�Ӵ��ݸ���һ��then,ͨ��then�����к����Ĳ������ո�ֵ


4 Promise ����API

1.ʵ������
p.then() �õ��첽������ȷ���
p.catch() ��ȡ�쳣��Ϣ
p.finally()�ɹ���񶼻�ִ�У���������ʽ��׼��

2.���󷽷�

Promise.all() �����������첽������������ִ����ɲ��ܵõ����

Promise.race()�����������첽����ֻ��һ��������ɾ��ܵõ����

Promise.all(p1,p2,p3).then((result)=>{
  console.log(result);

})
Promise.all(p1,p2,p3).then((result)=>{
  console.log(result);

})




















