fetch
1.��������

 ���Ӽ򵥵����ݻ�ȡ��ʽ�����ܸ�ǿ�󡢸������Կ���xhr��������
 ����Promiseʵ��

2.�﷨�ṹ
  fetch(url).then(fn2)
            .then(fn3)
            ....
            .catch(fn)

http://developer.mozilla.org/en-US/docs/Web/API/Fetch_API(fetch APIʹ��˵��)

3.�����÷�

fetch('http://localhost:3000/fdata').then(data=>{
return data.text();//text()��������fetch, �õ�����Promiseʵ������,���ڻ�ȡ��̨������
}).then(ret=>{

//ע������ŵõ���������

console.log(ret);

})

4 fetch �ӿڵ��÷��� 
fetch ������� 
get ��ʽȥ�������

1.fetch('/abc?id=123',{
method: 'get'

}).then(data=>{
return data.text();//text()��������fetch, �õ�����Promiseʵ������,���ڻ�ȡ��̨������
}).then(ret=>{

//ע������ŵõ���������

console.log(ret);

})

2.fetch('/abc/123',{
method: 'get'

}).then(data=>{
return data.text();//text()��������fetch, �õ�����Promiseʵ������,���ڻ�ȡ��̨������
}).then(ret=>{

//ע������ŵõ���������

console.log(ret);

})

DELETE��ʽ������� 
.fetch('/abc/123',{
method: 'delete'

}).then(data=>{
return data.text();//text()��������fetch, �õ�����Promiseʵ������,���ڻ�ȡ��̨������
}).then(ret=>{

//ע������ŵõ���������

console.log(ret);

})
POST����ʽ�Ĳ�������

fetch('/abc/123',{
method: 'post',
body:'uname=lisi&pwd=123',
headers:{

   'Content-Yype':'application/x-www-form-urlencoded',//������

}

}).then(data=>{
return data.text();//text()��������fetch, �õ�����Promiseʵ������,���ڻ�ȡ��̨������
}).then(ret=>{

//ע������ŵõ���������

console.log(ret);

})

fetch('/abc/123',{
method: 'post',
body:JSON.strinhify({
 uname:'����'��
 pwd:12,
}),
headers:{

   'Content-Yype':'application/json',//������

}

}).then(data=>{
return data.text();//text()��������fetch, �õ�����Promiseʵ������,���ڻ�ȡ��̨������
}).then(ret=>{

//ע������ŵõ���������

console.log(ret);

})
��̨�ӿ�
// POST�����������12 
app.post('/abc/123',(req,res)=>{
res.send('POST���������'+req.body.uname+req.body.pwd)

})

put �������

fetch('/abc/123',{
method: 'put',
body:JSON.strinhify({
 uname:'����'��
 pwd:12,
}),
headers:{

   'Content-Yype':'application/json',//������

}

}).then(data=>{
return data.text();//text()��������fetch, �õ�����Promiseʵ������,���ڻ�ȡ��̨������
}).then(ret=>{

//ע������ŵõ���������

console.log(ret);

})
��̨�ӿ�
// POST�����������12 
app.post('/abc/123',(req,res)=>{
res.send('POST���������'+req.body.uname+req.body.pwd)

})