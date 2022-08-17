## Project-related API



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

  
