# 查看volume內檔案

想要查看細部資訊可以使用 inspect 指令。由於此例是在 linux 環境中，因隔了一層 docker 自己的  VM 所以不會直接映射在實體 Windows 資料夾路徑中。
```
docker volume inspect {volume-name}
```

若是使用 WSL2 (Windows Subsystem for Linux) 來執行 Docker 時，可在以下路徑找到所有 volume 資料。
```
\\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes
```

###### tags: `Docker`