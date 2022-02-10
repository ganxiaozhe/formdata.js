# FormData.js
基于 gQuery 实现的 FormData 封装，用于 node.js 无浏览器环境下发起 POST 请求。


# Useage
```javascript
let $fd = new $.formdata();
$fd.append('key1', 'value');
$fd.append('key2', {a:1, b:2, file:new Blob()});
$fd.append('key3', [1,2,3,4,5]);

async function doFetch(url, bodyMH){
    return fetch(url, {
        headers:{
            'Content-Type': $fd._getContentType()
        },
        body: await $fd.toBuffer()
    }).then(rsp=>{
        if(!rsp.ok){throw new Error('Network response was not ok.');}
        return rsp[bodyMH]();
    }).catch(err => {
        throw new Error(err);
    });
};
doFetch('https://gquery.org', 'text').then(rsp=>{
    console.log(rsp);
});
```
