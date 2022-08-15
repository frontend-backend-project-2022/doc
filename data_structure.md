# 数据结构文档

---

### 后端sqlite表结构

* users表

  ```sqlite
  TABLE users
  
  ​      (
  
  ​        id INTEGER PRIMARY KEY AUTOINCREMENT,
  
  ​        username TEXT NOT NULL,
  
  ​        pwhash TEXT NOT NULL
  
  ​      )
  ```

* containers表

  ```sqlite
  TABLE containers
  
  ​      (
  
  ​        id INTEGER PRIMARY KEY AUTOINCREMENT,
  
  ​        containerid TEXT NOT NULL,
  
  ​        projectname TEXT,
  
  ​        time DATETIME NOT NULL,
  
  ​        language TEXT NOT NULL,
  
  ​        version TEXT NOT NULL,
  
  ​        userid INTEGE,
  
  ​        FOREIGN KEY(userid) REFERENCES users(id) on delete cascade
  
  ​      )
  ```

  ---
  
  ### 后端xterm(terminal)在内存中的数据
  
  * socket_poll是一个字典，保存request.sid到xtermData类的映射
  * xtermData类保存pty，terminal (xterm.py:11-17)
    * pty是pty.openpty()创建的master终端，可通过它与container交互
    * terminal是subprocess.Popen()创建的docker exec子进程
  
  ---
  
  ### 后端pdb在内存中的数据
  
  * pdb_poll是一个字典，保存request.sid到pdbData类的映射
  * pdbData类保存bp，containerid，filepath，psocket，lineno，state (debugger.py:10-21)
    * bp是断点列表，bp[n]=lineno下标表示第(n+1)个断点位于第lineno行（n+1是因为断点编号从1开始而列表从0开始），注意某一行可能有多个断点。删除断点后bp对应位置的值修改为-1。
    * filepath是该python文件相对于/workspace的路径
    * lineno是当前运行到第lineno行
    * state=0表示debug中断，state=1表示pdb正在运行
  * 每次socketio请求后均会emit message事件，每次message事件中均会包含bp，lineno，state和可选的message备注信息
  
  ### 
  
  
  
  

