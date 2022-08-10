## Project-related API

上传文件

* `GET /docker/uploadFile/`

* multipart/form-data

  ```json
  {
      "file" :  //要上传的文件,
      "dir" : "./", //workspace内的相对路径
      "containerid" : "123456",
  }
  ```

* 注：文件名中不能含有'/'等特殊字符

* return: "success"

  

上传文件夹（未测试）

* `GET /docker/uploadFolder/`
* 与上传文件类似



下载文件内容

* `GET /docker/downloadContent/`

* request: json

  ```json
  {
      "filename" :  "NAME",
      "dir" : "./", //workspace内的相对路径
      "containerid" : "123456",
  }
  ```

* return: string (contents of file)



获取工程的文件结构

* `GET /docker/getdir/<container_id>`
* para: container_id
* return: json

```json
{
    "src": {
        "main.py": "",
        "modules": {
            "a.py": "",
            "b.py": "",
        }
    },
    "doc": {
        "report.md": ""
    }
}
```



创建工程

* `POST /database/createProject`
* request:

```json
{
    "projectname": "PROJECT",
    "language": "python",
    "version": "10",
}
```

* return: container_id



查询全部工程

* `GET /database/getAllProjects`
* request: None
* return: json (list of projects)

```json
[
    {
        "projectname":"PROJECT", 
     	"containeri":"123456", 
     	"language": "python", 
     	"version":"10", 
     	"time":"2022-08-06 22:32:43"
    },
    ...
]
```



查询单个工程

* `GET /database/getProject/<container_id>`
* para: container_id
* return: json

```json
{
    "projectname":"PROJECT", 
    "containerid":"123456", 
    "language": "python", 
    "version":"10", 
    "time":"2022-08-06 22:32:43"
}
```



删除工程

* `DELETE /database/deleteProject/<containerid> `
* para: containerid (str)
* return: "success"



修改工程名称

* `POST /database/updateProject`
* request:

```json
{
    "containerid" : "123456",
    "newname" : "NewName",
}
```

* return: "success"

  
