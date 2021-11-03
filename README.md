# wxcloudrun-django
微信云托管 django 框架模版


简介：Django (https://www.djangoproject.com/) 是一个开源的Web应用框架，由Python写成，鼓励简洁实用的设计和敏捷快速的开发方式。

详细介绍：

1. 本示例中，使用的是django 3.2.7，通过80端口对外。
   * 如需修改端口号，请到Dockerfile中修改。
   * 修改端口号之后，如果使用流水线部署版本，请确保container.config.json中的containerPort字段也同步修改；如果在微信云托管控制台手动「新建版本」，请确保“监听端口”字段与代码中端口号保持一致，否则会引发部署失败。
2. 在微信云托管控制台一键部署本示例，会同时自动开通环境内的MySQL服务并完成初始化，后续可直接使用。数据库的地址、帐号、密码会被作为环境变量默认注入，settings.py中直接引用。
   * 如不想使用微信云托管自带的MySQL，请手动修改settings.py中数据库信息并在微信云托管控制台注销MySQL。
   * 未通过一键部署按钮，而是直接使用本示例的代表进行部署，需要手动在微信云托管控制台中开通MySQL，且数据库信息不会默认注入。在新建版本时需要手动将数据库信息作为环境变量填入。
3. 基于示例二次开发操作步骤：
   * 在微信云托管控制台一键部署，完成服务创建、MySQL初始化、首个版本部署上线。
   * fork示例代码到自己的代码仓库，在此基础上进行二次开发。
   * 服务的第二个及后续版本，基于自己的代码仓库进行部署。
4. 代码仓库中的container.config.json文件仅用于在微信云托管中创建流水线。如果不使用流水线，而是用本项目的代码在微信云托管控制台手动「新建版本」，则container.config.json配置文件不生效。最终版本部署效果以「新建版本」窗口中手动填写的值为准。

示例API列表：

1 根据ID查询用户

* URL路径：
  ```/user/:id```
  
* 请求示例：
```
curl -X GET  http://{ip}:{port}/user/1
```

* 响应示例：
```
{
    "code": 0,
    "data": {
        "id": 34,
        "name": "1231231232131",
        "age": 10,
        "email": "m1779387qqwewqeqwe3123@163.com",
        "phone": "1779aqweqwea3873123@163.com",
        "description": "111",
        "create_time": "2021-11-03T12:25:13Z",
        "update_time": "2021-11-03T12:25:13Z"
    }
}
```


2 新增用户

* URL路径：
  ```/user```
  
* 请求示例：
```
curl http://{ip}:{port}/user \
  -X POST \
  -H 'Content-Type: application/json' \
  -d '{  
      "name":"1231231232131",
      "age":10,
      "email":"m1779387qqwewqeqwe3123@163.com",
      "phone":"1779aqweqwea3873123@163.com",
      "description":"111"
  }'
```

* 响应示例：
```
{
    "code": 0,
    "errorMsg": ""
}
```

3 根据ID修改用户

* URL路径：
  ```/user```
  
* 请求示例：
```
curl http://{ip}:{port}/user \
  -X PUT \
  -H 'Content-Type: application/json' \
  -d '{  
      "id":1,
      "name":"1231231232131",
      "age":10,
      "email":"m1779387qqwewqeqwe3123@163.com",
      "phone":"1779aqweqwea3873123@163.com",
      "description":"111"
  }'
```

* 响应示例：
```
{
    "code": 0,
    "errorMsg": ""
}
```

4 根据ID删除用户

* URL路径：
  ```/user/:id```
  
* 请求示例：
```
curl http://{ip}:{port}/user/1 \
  -X DELETE \
  -H 'Content-Type: application/json' \
  -d '{   }'
```

* 响应示例：
```
{
    "code": 0,
    "errorMsg": ""
}
```
