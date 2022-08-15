## socketio-related API

采用socketio的部分有terminal和pdb，下介绍pdb的API

* 注：全部均未经过调试（08/15）
* 注：发送事件应该分多个，待完成（08/15）



### 发送事件

* 发送"response"事件，并返回如下值

  * bp是断点列表，bp[n]=lineno下标表示第(n+1)个断点位于第lineno行（n+1是因为断点编号从1开始而列表从0开始），注意某一行可能有多个断点。删除断点后bp对应位置的值修改为-1。
  * lineno是当前运行到第lineno行
  * state=0表示debug中断，state=1表示pdb正在运行
  * message是备注信息，在以下各个事件中有注明

* 返回json如下：

  ```json
  {
      'bp': [3,1,3,-1,5,-1], 
   	'lineno': 3,
      'state': 1,
      'message': 'xxx',
  }
  ```



### 接收事件

建立连接：

* 接收"connectSignal"事件，需要container_id与filepath两个参数
  * container_id(str)，项目的container id
  * filepath(str)，调试文件相对于workspace的路径

添加断点：

* 接收"add"事件，需要给予lineno参数
  * lineno(int)，断点位于的行数

删除断点：

* 接收"delete"事件，需要给予lineno参数
  * lineno(int)，断点位于的行数

跳到下一个断点

* 接收“skip”事件
* 返回message为在控制台获得的输出(str)

跳到下一行

* 接收“next”事件
* 返回message为在控制台获得的输出(str)

查看参数和参数类型

* 接收“check”事件，需要给予variables参数

  * variables是一个list，即需要查看的参数名（待修改 08/15）

* 返回message如下

  ```json
  [
      {
   		"name" : "a",
           "value" : "1",
           "type" : "<class 'int'>",
      },
      ...
  ]
  ```

强行退出

* 接收“exit”事件