# Docker常用指令

取得image
```
docker pull image名稱
```
使用hash digest
```
docker pull image名稱@sha256:完整hash digest
```

移除現有容器啟動新容器
```
docker run -it --rm -p 8000:80 --name 容器名稱 image名稱
```
-it：使用虛擬終端機
--rm：移除現有容器
-p：主機的port對應容器的port(主機port:容器port)
--name：容器名稱

列出所有 Docker 容器
```
docker ps -a
```
-a 為所有狀態，包含停止的容器

啟動
```
docker start 容器ID/容器名稱
```

停止
```
docker stop 容器ID/容器名稱
```

強制停止
```
docker kill 容器ID/容器名稱
```

重新啟動
```
docker restart 容器ID/容器名稱
```

暫停
```
docker pause 容器ID/容器名稱
```

從暫停中恢復啟動
```
docker unpause 容器ID/容器名稱
```

內外資料映射
將容器內的指定資料夾對應到本機的指定資料夾，會自動同步
```
docker run -v <外部絕對路徑>:<內部路徑> <ImageName>
```

###### tags: `Docker`