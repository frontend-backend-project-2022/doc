## socketio-related API

采用socketio的部分有terminal和pdb，下介绍pdb的API

* 注：全部均未经过调试（08/15）



### 发送事件

* 发送"response"事件，并返回如下值

  * bp是断点列表
  * lineno是当前运行到第lineno行
  * state=0表示debug中断，state=1表示pdb正在运行
  * messageType为message的类型，分为console（控制台输出），variables（变量值查看）和none（无message，message默认为空字符串）
  * message是备注信息，在以下各个事件中有注明

* 返回json如下：

  ```json
  {
      'bp': [1,3,4], 
   	'lineno': 3,
      'state': 1,
      'messageType' : 'console', // console/variables/none
      'message': 'xxx', // empty string for 'none'
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
* 返回message为在控制台获得的输出(str)，messageType为"console"

跳到下一行

* 接收“next”事件
* 返回message为在控制台获得的输出(str)，messageType为"console"

查看参数和参数类型

* 接收“check”事件，需要给予variables参数

  * variables是一个json，即需要查看的参数名

    ```json
    ['a', 'cnt', ]
    ```

* 返回message如下，messageType为"variables"

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