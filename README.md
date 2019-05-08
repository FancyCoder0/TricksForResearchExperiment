# TricksForResearchExperiment

## 跑程序时注意的问题

- 内存不够 Out of Memory

- 磁盘写满的问题 

## Linux实用命令

- 按时间顺序列出文件 ```ls -l -rt```

- 杀死包含$name的进程 ```ps aux | grep $name | awk '{print $2}' | xargs kill -9```

- 查看硬盘空间 ```df -h```

- Linux中查看各文件夹大小命令 ```du -h --max-depth=1```

- ```cp "$file1" "$file2"``` （防止路径中存在空格的情况）

## Tmux Cheat Sheet


```
# 列表：tmux ls
# 新建：tmux new -s $new_window_name
# 进入：tmux a -t $window_name
# 分屏：Ctrl+B "
# 分屏：Ctrl+B %
# 退出：Ctrl+B d
# 关闭: Ctrl+B x
```

## Linux解压缩 Cheat Sheet

### zip
```zip -r $name.zip $filefolder```
```unzip $name.zip```

(TODO) 除去哪些文件：

### tar
TODO

记录屏幕输出: $job | tee

## python cheat sheet

### 命令行参数解析

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



