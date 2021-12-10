# Docker基础




## 下载安装

> Environment: Ubuntu18.04
>
> Reference: https://docs.docker.com/engine/install/ubuntu/


```bash
# 卸载 docker
sudo apt-get remove docker docker-engine docker.io containerd runc
```


```bash
sudo apt-get update

sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
    
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64]  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" 

# docker version list
apt-cache madison docker-ce
apt-cache madison docker-ce-cli

# install
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```



```bash
# 安装指定版本
sudo apt-get install docker-ce=5:18.09.9~3-0~ubuntu-bionic docker-ce-cli=5:18.09.9~3-0~ubuntu-bionic containerd.io
```



```bash
# 设置 daemon.json
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
EOF
```



```bash
# reboot docker
sudo systemctl daemon-reload
sudo systemctl restart docker
```



```bash
# start up automatically on boot up
sudo systemctl enable docker && sudo systemctl start docker
```



```bash
# docker permission deny
sudo groupadd docker
sudo gpasswd -a [user name] docker
sudo service docker restart
```



## 修改存储位置

```bash
// 修改docker默认镜像/容器存储位置
// Docker默认的镜像和容器存储位置在/var/lib/docke

1)修改docker.service文件　
cd /etc/systemd/system/multi-user.target.wants
sudo vim docker.service

// ExecStart=/usr/bin/dockerd --graph=/data/docker --storage-driver=overlay

--graph=/data/docker：docker新的存储位置
--storage-driver=overlay ： 当前docker所使用的存储驱动

2) 重启docker　
sudo systemctl daemon-reload
sudo systemctl restart docker
```



## Docker常用操作

```sh
# docker --help
build       Build an image from a Dockerfile
commit      Create a new image from a container's changes
cp          Copy files/folders between a container and the local filesystem
create      Create a new container
diff        Inspect changes to files or directories on a container's filesystem
events      Get real time events from the server
exec        Run a command in a running container
export      Export a container's filesystem as a tar archive
history     Show the history of an image
images      List images
import      Import the contents from a tarball to create a filesystem image
info        Display system-wide information
inspect     Return low-level information on Docker objects
kill        Kill one or more running containers
load        Load an image from a tar archive or STDIN
login       Log in to a Docker registry
logout      Log out from a Docker registry
logs        Fetch the logs of a container
pause       Pause all processes within one or more containers
port        List port mappings or a specific mapping for the container
ps          List containers
pull        Pull an image or a repository from a registry
push        Push an image or a repository to a registry
rename      Rename a container
restart     Restart one or more containers
rm          Remove one or more containers
rmi         Remove one or more images
run         Run a command in a new container
save        Save one or more images to a tar archive (streamed to STDOUT by default)
search      Search the Docker Hub for images
start       Start one or more stopped containers
stats       Display a live stream of container(s) resource usage statistics
stop        Stop one or more running containers
tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
top         Display the running processes of a container
unpause     Unpause all processes within one or more containers
update      Update configuration of one or more containers
version     Show the Docker version information
wait        Block until one or more containers stop, then print their exit codes
```



```sh
# docker build --help
Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Run a command in a new container

Options:
 	  --add-host list                  Add a custom host-to-IP mapping (host:ip)
  -d, --detach                         Run container in background and print container ID
  -e, --env list                       Set environment variables
      --gpus gpu-request               GPU devices to add to the container ('all' to pass all GPUs)
      --help                           Print usage
  -h, --hostname string                Container host name
  -i, --interactive                    Keep STDIN open even if not attached
  -m, --memory bytes                   Memory limit
      --mount mount                    Attach a filesystem mount to the container
      --name string                    Assign a name to the container
      --network network                Connect a container to a network
      --privileged                     Give extended privileges to this container
  -p, --publish list                   Publish a container's port(s) to the host
      --rm                             Automatically remove the container when it exits
      --shm-size bytes                 Size of /dev/shm
  -t, --tty                            Allocate a pseudo-TTY
      --ulimit ulimit                  Ulimit options (default [])
  -u, --user string                    Username or UID (format: <name|uid>[:<group|gid>])
  -v, --volume list                    Bind mount a volume
  -w, --workdir string                 Working directory inside the container
```



Examples

```bash
# list all containers 
docker container ls -a / docker ps -a

# list all containers id
docker container ls -aq / docker contaier ls -a | awk {'print$1'}

# remove all containers
docker rm $(docker container ls -aq)

# list all exited containers
docker container ls -f "status=exited"

# list all exited containers id
docker container ls -f "status=exited" -q
docker ps -a|grep Exited|awk '{print $1}'

# remove all exited containers
docker rm $(docker container ls -f "status=exited" -q)
docker rm `docker ps -a|grep Exited|awk '{print $1}'`
docker rm $(docker ps -qf status=exited)

```



```bash
#删除名称或标签为none的镜像
docker rmi -f  `docker images | grep '<none>' | awk '{print $3}'`
#删除所有名字中带 “dee” 关键字的镜像
docker rmi $(docker images | grep "dee" | awk '{print $3}') 
```



```bash
# docker commit [CONTAINER] [REPOSITORY]
docker run -d -it --name nginx nginx
docker commit nginx hisunyh/my-nginx:1.0
```



```sh
docker run -d -it --name crawler --add-host master.namenode:192.168.1.25 --add-host slave.datanode1:192.168.1.26 --add-host slave.datanode2:192.168.1.29 -e "queue_names=for_get_tb_detail" dee_crawler:1.0
```



container export/import

```bash
# docker export [OPTIONS] CONTAINER
# [OPTIONS] --output , -o

docker export crawler > crawler-export.tar
# or
docker export --output="crawler-export" crawler

# docker import [OPTIONS] file|URL|- [REPOSITORY[:TAG]]
docker import crawler-export.tarr dee_crawler_export:1.0
```



image save/load

```bash
# docker save [OPTIONS] IMAGE [IMAGE...]
# [OPTIONS] --output , -o

docker save -o dee_crawler_save.tar dee_crawler:1.0
# or
docker save dee_crawler:2.0 > dee_crawler_save.tar

scp dee_crawler_save.tar user@host:/tmp/dee_crawler_save.tar

# docker load [OPTIONS]
# [OPTIONS] --input , -i
docker load < dee_crawler_save.tar
docker load --input dee_crawler_save.tar
```



## Dockerfile

> Refenence:
>
> https://docs.docker.com/engine/reference/builder/
>
> https://docs.docker.com/develop/develop-images/dockerfile_best-practices/



Samples

```bash
sudo tee ./Dockerfile.dev <<-'EOF'
FROM golang:1.14-alpine AS prod-build
ENV GOPROXY https://goproxy.cn,direct
# ENV GO111MODULE on
WORKDIR /workspace
COPY . /workspace
RUN CGO_ENABLED=0 GOOS=linux go build -o deep_arena .

# FROM scratch AS prod-final
FROM debian:9.12 AS prod-final
RUN rm -f /etc/localtime \
&& ln -sv /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
&& echo "Asia/Shanghai" > /etc/timezone

COPY --from=prod-build /workspace/deep_arena .
COPY --from=prod-build /workspace/conf.toml .
COPY --from=prod-build /workspace/config .
EXPOSE 8082
CMD ["/deep_arena"]
EOF

docker login my-horbor.com

docker build -f ./Dockerfile.dev -t my-horbor.com/deep_arena:dev_v1.0 .

docker push my-horbor.com/deep_arena:dev_v1.0
docker pull my-horbor.com/deep_arena:dev_v1.0

docker run -d -it -p 9082:8082 --name da -v ~/pod_logs:/pod_logs my-horbor.com/deep_arena:dev_v1.0
```




