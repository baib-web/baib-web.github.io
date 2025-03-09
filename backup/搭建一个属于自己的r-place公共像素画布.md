# 安装git
```
sudo apt update
sudo apt install git
```
# 安装go编译
`sudo apt-get update && sudo apt-get -y install golang-go `
# 拉取代码
`git clone https://ghfast.top/https://github.com/rbxb/place.git`
# 更换国内镜像
`go env -w GOPROXY=https://goproxy.cn,direct`
# 编译place-go
```
cd ./place
go build cmd/place/place.go
```
# 运行 place 并将-root参数设置为web/root目录的位置。
`./place -root web/root -port :8080`