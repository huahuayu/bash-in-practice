# bash-by-examples

## hello world

`hello-world.sh`

```bash
#!/bin/bash
echo "Hello World"
```

执行方式 1：`bash hello-world.sh`

执行方式 2：`./hello-world.sh`（需要有执行权限）

如果缺少权限，使用 chmod 增加权限：`chmod a+x hello-world.sh`

## echo

`echo`命令有很多选项来打印字符串到终端，`echo`默认打印时会带换行，类似于 java 的`println`；`-n`选项不换行，类似于`print`；`-e`则会解释转义字符

`echo-example.sh`

```bash
#!/bin/bash
echo "Printing text with newline"
echo -n "Printing text without newline"
echo -e "\nRemoving \t backslash \t characters\n"
```

## 注释

使用`#`来单行注释

`comment_example.sh`

```bash
#!/bin/bash

# Add two numeric value
((sum=25+35))

#Print the result
echo $sum
```

多行注释可以用`: ' 注释内容 '`来表达

`multiline-comment.sh`

```bash
#!/bin/bash
: '
The following script calculates
the square value of the number, 5.
'
((area=5*5))
echo $area
```

## while

`while-example.sh`

```bash
#!/bin/bash
count=0
while [ $count -lt 5 ]
do
    echo $count
    ((count++))
done
```

`while-infinite-loop.sh`

```bash
#!/bin/bash
while :
do
    echo 'never stop'
done
```

`while` 语句可以写为一行，用分号隔开。大多数 bash 语句可以写为一行，但是可读性不好。

`while-in-one-line.sh`

```bash
#!/bin/bash
count=0
while [ "$count" -lt 5 ]; do echo $count; ((count++)); done
```

## 单中括号和双中括号区别

- 单中括号 [ ]
  a. [ ] 两个符号左右都要有空格分隔（否则报错）
  b. 内部操作符与操作变量之间要有空格：如 [ "a" = "b" ]
  c. 字符串比较中，> < 需要写成> \< 进行转义
  d. [ ] 中字符串或者\${}变量尽量使用”” 双引号扩住，以避免值未定义引用而出错
  e. [ ] 中可以使用 –a –o 进行逻辑运算
  f. [ ] 是 bash 内置命令：[ is a shell builtin

- 双中括号
  a. [[ ]] 两个符号左右都要有空格分隔（否则报错）
  b. 内部操作符与操作变量之间要有空格：如 [[ "a" = "b" ]]
  c. 字符串比较中，可以直接使用 > < 无需转义
  d. [[ ]] 中字符串或者\${}变量尽量使用”” 双引号扩住，如未使用”“会进行模式和元字符匹配
  e. [[ ]] 内部可以使用 && || 进行逻辑运算
  f. [[ ]] 是 bash keyword：[[ is a shell keyword

## test

`test-dir-exists.sh`

```bash
#!/bin/bash
if [ -e /tmp ]
then
    echo "dir exists!"
else
    echo "dir not exists"
fi

# if [ -e /tmp  ]; then echo "dir exists!"; else echo "dir not exists" fi
```

常用测试

```text
     -b file       True if file exists and is a block special file.

     -c file       True if file exists and is a character special file.

     -d file       True if file exists and is a directory.

     -e file       True if file exists (regardless of type).

     -f file       True if file exists and is a regular file.

     -g file       True if file exists and its set group ID flag is set.

     -h file       True if file exists and is a symbolic link.  This operator is retained for compatibility with previous versions of this program.  Do not rely on
                   its existence; use -L instead.

     -k file       True if file exists and its sticky bit is set.

     -n string     True if the length of string is nonzero.

     -p file       True if file is a named pipe (FIFO).

     -r file       True if file exists and is readable.

     -s file       True if file exists and has a size greater than zero.

     -t file_descriptor
                   True if the file whose file descriptor number is file_descriptor is open and is associated with a terminal.

     -u file       True if file exists and its set user ID flag is set.

     -w file       True if file exists and is writable.  True indicates only that the write flag is on.  The file is not writable on a read-only file system even if
                   this test indicates true.

     -x file       True if file exists and is executable.  True indicates only that the execute flag is on.  If file is a directory, true indicates that file can be searched.

     -z string     True if the length of string is zero.

     -L file       True if file exists and is a symbolic link.

     -O file       True if file exists and its owner matches the effective user id of this process.

     -G file       True if file exists and its group matches the effective group id of this process.

     -S file       True if file exists and is a socket.

     file1 -nt file2
                   True if file1 exists and is newer than file2.

     file1 -ot file2
                   True if file1 exists and is older than file2.

     file1 -ef file2
                   True if file1 and file2 exist and refer to the same file.

     string        True if string is not the null string.
```

## for

```bash
#!/bin/bash
for(())
```

## 验证安装

`validate-prereqs.sh`

```bash
#!/bin/bash

echo "============== Validate Docker =========="
docker version
docker images
echo "========== Validate Docker Compose ======"
docker-compose  version

echo "============== Validate version =========="
go version

echo "============== GOPATH =========="
echo $GOPATH

echo "============== Fabric =========="
peer version
orderer version

echo "============== Fabric CA ======="
fabric-ca-client version
fabric-ca-server version
```
