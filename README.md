# TricksForResearchExperiment

## Linux实用命令

- timeout(最靠谱的可以kill进程的方式) ``` timeout $seconds $job ```

- 按时间顺序列出文件 ```ls -l -rt```

- 杀死包含$name的进程 ```ps aux | grep $name | awk '{print $2}' | xargs kill -9```

- 查看硬盘空间 ```df -h```

- Linux中查看各文件夹大小命令 ```du -h --max-depth=1```

- ```cp "$file1" "$file2"``` （防止路径中存在空格的情况）

- 记录屏幕输出: ``` $job | tee ```

## Tmux Cheat Sheet

```
# 列表：tmux ls
# 新建：tmux new -s $new_session_name
# 进入：tmux a -t $session_name
# 关闭：tmux kill-session -t $session_name
# 新建并运行程序： tmux new-window -n:$new_window_name '$job'

# 分屏：Ctrl+B "
# 分屏：Ctrl+B %
# 分离：Ctrl+B d
# 关闭窗口: Ctrl+B x
```

## Linux解压缩 Cheat Sheet

### zip
```zip -r $name.zip $filefolder```

```unzip $name.zip```

(TODO) 除去哪些文件

### tar
TODO


## python cheat sheet

### 命令行参数解析

```
import sys

x = sys.argv[1]
```

### 文件读入

### 文件安全写入

```
def write_to_file(file, obj):
    path = os.path.dirname(file)
    if not os.path.exists(path):
        os.makedirs(path)
    with open(file, 'w') as write_file:
        write_file.write(obj)
    print('finish write %s to file....' % file)
```


### 执行系统命令行
```
os.system('echo 1')

def exe_cmd(cmd):  # 返回结果
    # print(cmd)
    r = os.popen(cmd)  
    text = r.read()  
    r.close()  
    return text 
print(exe_cmd('echo 1'))
```

### json
```
result = json.load(f) # 导入

with open(file, 'w') as f: # 导出
    f.write(json.dumps(obj))
```

### xml

### 多线程 多进程

```
from multiprocessing import Pool
# ....
# arr = [1,2,3]
def work(x):
  pass

with Pool(processes=10) as pool:
    result = pool.map(work, arr)
```
### 设置超时


## java cheat sheet

### 命令行参数解析

### 文件读入

### 文件安全写入

### 执行系统命令行

### json

### xml

### 多线程 多进程

### 设置超时


---
2019.05.09

记录一下本次做实验过程中遇到的问题和心得，供大家参考。

实验的内容大致为要先从GitHub上下载大量代码的历史版本然后组成实验cases，然后运行程序看cases的准确率之类的。

1. 数据集由若干项目子集组成。我开始没有注意到每个项目的大小，开始只跑了最小的几个，导致后面跑大的时候措手不及。建议实验前对项目总体情况有个了解。
2. 爬数据，就是一堆http request，我开始就写了一个for循环，加上国内爬GitHub网速慢。发现小的项目一晚上，就决定忍忍，后来发现大项目根本跑不完。解决：换成并发+美国服务器 建议：像这种http request并发可以显著提高效率。
3. 运行实验。
	3.1 程序要提供良好的命令行接口，然后可以利用脚本语言方便运行。 
	3.2 程序鲁棒性：异常处理、超时设置、写log、可重启
	3.3 要考虑到内存（Out of Memory），硬盘（磁盘写满）等问题  (这次全被我遇到了....)
	3.4 提高自动化程度
		3.4.1 利用tmux等工具 tmux可支持新建窗口并运行程序 ``` tmux new-window -n:mywindow1 'sleep 100' ```
		3.4.2 不太习惯vim的话就直接sshfs本地开编辑器改服务器程序
		3.4.3 工欲善其事必*先*利其器 先考虑能不能自动化或利用方便处理过程 再去做事
		3.4.4 熟悉常用的处理数据方法 json xml
	3.5 timeout 使用Liunx自带的 可以保证到时间kill进程 目前跑多任务 倾向Python Multi Processing + Linux timeout
