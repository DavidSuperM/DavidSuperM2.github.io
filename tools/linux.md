## 1.查看所有端口
```
netstat -ntlp
```

## 2.查看特定端口
```
lsof -i:5005
```

## 3.杀掉端口对应的进程
```
kill -9 5005
```

## 4.终端连接远程服务器
```
ssh 用户名@服务器地址
[输入密码]
```

## 5.查看服务器进程
```
ps -ef    //-e 显示每个现在运行的进程 -f 生成一个完全的列表
ps -ef | grep python    //筛选出有python关键字的     
```

## tail -200f log.txt
## 不滚动查看最后20行
不滚动并且grep查看最后20行

## 打印匹配行的前后10行
```
grep -10 ‘123’ test.log
```
## 连接mysql
```
mysql -h host -P 8008 --default-character-set=utf8 -u user -p pdw -D DBname;
```

## 导出mysql表数据

```

select * from pirate_book_chapter_update into outfile /tmp/project/chapter.xls //需要有权限

mysqldump -u[Mysql用户名] -h[mysqlIP] -P[mysql端口] -p[mysql密码] --default-character-set=utf8 --skip-opt --create-options -q -B --databases [库名] --tables [表名] --skip-tz-utc >>/tmp/project/table.sql
//--skip-tz-utc 是因为不加的话，导出来的timestamp时间会少8个小时
```

## 后台执行python脚本
```
nohup python -u run.py > run.out 2>&1 &
[1] 25584
```

## linux设置环境变量（未验证）
1.对当前用户生效
vim ~/.bash.profile
HOSTNAME = '/usr/bin/hostname 2>/dev/null'   // 得到 9-151-18-99
export CLASSPATH=./JAVA_HOME/lib;$JAVA_HOME/jre/lib
source ~/.bash_profile    //让环境 变量立即生效，不然就是下次重启生效

2.对所有用户生效
vim /etc/profile    
export CLASSPATH=./JAVA_HOME/lib;$JAVA_HOME/jre/lib
source /etc/profile

## crontab定时任务
```
 crontab -e
//编辑文件，添加下面一行语句，作用：每分钟执行一次脚本
* * * * cd /tmp/project/ && sh ./monitor.sh >./shell_log.txt 2>&1   
```
语句复制进去的可能不能保存成功，需要手打，因为复制进去的可能会有乱码不合适的字符看不见

## SecureCRT操作
```
Ctrl + a ：移到命令行首
Ctrl + e ：移到命令行尾
Ctrl + xx：在命令行首和光标之间移动

Ctrl + u ：从光标处删除至命令行首
Ctrl + k ：从光标处删除至命令行尾
Ctrl + w ：从光标处删除至字首
```

1.  上传本地文件到服务器
```
cd /tmp
rz  //然后会弹出弹窗选择本地的文件
//文件传输也可以用sftp：右击此会话的标签栏，选择“连接SFTP会话”
//put [本地文件的地址] [服务器上文件存储的位置]
//get [服务器上文件存储的位置] [本地要存储的位置]
```
2. 下载服务器文件到本地
```
sz  filename   //下载到默认地址
```
默认地址设置：
Options->Session Options->Terminal->X/Y/ZModem->Download

3.双击复制并打开新session:
options -> global options -> Terminal -> Tabs 选择Double-click action的下拉框为Clone tab，这样就可以在已经打开的session标签中鼠标双击，打开一个完全一样的新session标签。 

4.保持连接：
options -> global options -> General -> Default Session,点击Edit default settings按钮，在Terminal中钩上Send protocol NO-OP, every 30 seconds，这样可以保证securecrt不会因为一段时间没有操作，而丢掉连接。

5. 按钮栏保存常用命令
点击查看（view）-> 按钮栏（Button Bar）
此时SecureCRT窗户底下会出现一条横杠。右击它，会出现“新建按钮”的选项。