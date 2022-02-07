# imgUrl Api 后端开发文档

> A chart bed for your own use

> 需要授权的 API ，必须在请求头中使用 Authorization 字段提供 token 令牌

> 使用 HTTP Status Code 标识状态

> 数据返回格式统一使用 JSON 


## 状态码
|状态码|含义|说明|
|--|--|--|
|200|OK|请求成功|
|403|鉴权错误|参数已存在, token 过期|
|403|请求的资源不存在|参数找不到或者不存在, token 错误|
|422|参数缺失|上传表单数据缺失|

## 登录注册

### 注册验证接口

+ 请求路径: http://waite.mingol.cn/user/register
+ 请求方式: 'POST', 'GET'
+ 请求参数 
  |参数名|参数说明|备注| 
  |--|--|--| 
  |phone|手机号码|不能为空| 
  |name|用户名|不能为空| 
  |password|密码|不能为空|
+ 响应
    ```
    { "msg": "注册成功", "status": "200"}`
    ```


### 登录验证接口
+ 请求路径: http://waite.mingol.cn/user/login
+ 请求方式: 'POST', 'GET'
+ 请求参数
  |参数名|参数说明|备注|
  |--|--|--|
  |user|用户名或者手机号码|不能为空|
  |password|密码|不能为空|
+ 响应参数
  |参数名|参数说明|备注|
  |--|--|--|
  |name|用户名||
  |phone|手机号码||
  |permission|用户权限||
  |token|令牌|基于 jwt 的令牌|
+ 响应
    ```
    {
        "data": {
            "name": "waite",
            "permission": 10,
            "phone": "13232594494",
            "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2NDQyMjk0MzQuOTM4NDE0NiwiaWF0IjoxNjQ0MjI1ODM0LjkzODQxNjIsImlzcyI6IndhaXRlIiwiZGF0YSI6eyJwaG9uZSI6IjEzMjMyNTk0NDk0IiwibmFtZSI6IndhaXRlIiwicGVybWlzc2lvbiI6MTB9fQ.iGvZVXtSQuWHgNUvZGCwC3AkMGUAVViQ2bGJ7VENBp4"
        },
        "msg": "登录成功",
        "status": "200"
    }
    ```


## 图片

### 上传图片
+ 请求路径: http://waite.mingol.cn/picture/upload
+ 请求方式: 'POST'
+ 请求参数
  |参数名|参数说明|备注|
  |--|--|--|
  |file|文件|只能上传png,PNG,jpg,JPG,jpeg,JPEG,gif,GIF类型的文件|
  |fileName|自定义的文件名字|可以为空, 默认命名为 Md5 |
  |fileDetail|文件描述|可以为空|
+ 响应
    ```
    { "msg": "上传图片成功", "status": "200"}`
    ```
  

  
### 获取图片
+ 请求路径: http://waite.mingol.cn/picture/pictures
+ 请求方式: 'POST', 'GET'
+ 请求参数
  |参数名|参数说明|备注|
  |--|--|--|
  |query|查询参数|可以为空|
  |pageNum|当前页码|不能为空|
  |pageSize|每页显示条数|不能为空|
+ 响应参数
  |参数名|参数说明|备注|
  |--|--|--|
  |data|照片数据集合||
  |total|总记录数||
+ 响应
```
   {
    "data": {
        "data": [
            {
                "imgMd5": "1ef1669cf51731357ad7dbe9b48aef8f.jpg",
                "imgDetail": "",
                "imgId": 1,
                "imgName": "mm.jpg",
                "imgPath": "/www/project/imgUrl/public\\1ef1669cf51731357ad7dbe9b48aef8f.jpg",
                "imgUrl": "http://waite.mingol.cn//picture/show/1ef1669cf51731357ad7dbe9b48aef8f.jpg",
                "uploadTime": "1644221987",
                "uploadUser": "waite"
            }
        ],
        "total": 1
    },
    "msg": "获取照片成功",
    "status": 200
    }
```



### 图片预览以及下载
+ 预览请求路径: http://waite.mingol.cn/picture/show/{pictures.md5Name}
+ 下载请求路径: http://waite.mingol.cn/picture/down/{pictures.md5Name}
