## ide-related API

上传文件

* `POST /docker/uploadFile/`

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

上传文件夹

* `POST /docker/uploadFolder/`

* 与上传文件类似

上传文件内容

* `POST /docker/uploadFolder/`

* request: json

* ```json
  {
          'filename':'test.py',
          'dir':'hsu1023/new',
          'content':'print("hello world")',
          'containerid':"123456"
  }
  ```

* 注：可以在dir中包含未进行mkdir的内容，会自动创建

下载文件

* `GET /docker/downloadFile/`

* request: json
  
  ```json
  {
          'dir':'hsu1023/new',
          'filename':'test.py',
          'containerid':"123456"
  }
  ```

* return: file

下载文件夹

* `GET /docker/downloadFolder/`

* request: json
  
  ```json
  {
      "dir" : "./", //workspace内的相对路径
      "containerid" : "123456",
  }
  ```

* return: tar压缩文件

下载文件内容

* `POST /docker/uploadFolder/`

* request: json

* ```json
  {
          'filename':'test.py',
          'dir':'hsu1023/new',
          'content':'print("hello world")',
          'containerid':"123456"
  }
  ```

* return: str

新建文件夹（未测试）

* `POST /docker/createFolder/`

* request: json
  
  ```json
  {
      'dir':'hsu1023/new',
      'containerid':"123456"
  }
  ```

* 注：须一个个创建，dir的basename为新创建的文件夹

删除文件夹（及内容）

* `POST /docker/deleteFolder/`

* request: json
  
  ```json
  {
      'dir':'hsu1023/new',
      'containerid':"123456"
  }
  ```

新建文件

* `POST /docker/createFile/`

* request: json
  
  ```json
  {
      'dir':'hsu1023/new',
      'filename': "1.py",
      'containerid':"123456"
  }
  ```

删除文件

* `DELETE /docker/deleteFile/`

* request: json
  
  ```json
  {
      'dir':'hsu1023/new',
      'filename': "1.py"
      'containerid':"123456"
  }
  ```

重命名文件

* `POST /docker/renameFile/`

* request: json
  
  ```json
  {
      'dir':'.',
      'filename': "123.txt",
      'newname': "234.txt",
      'containerid':"123456"
  }
  ```

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
