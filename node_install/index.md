# node安装配置


nvm,npm,nrm

<!--more-->

### nvm

[nvm git](https://github.com/nvm-sh/nvm)

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash

source .bashrc

nvm --version
nvm ls-remote
nvm install 10.16.0
which node

nvm list
nvm use 10
nvm alias default 10

nvm reinstall-packages 10
```



### npm

```shell
npm -v
npm install -g npm    // -P  -D  -g

```



### nrm

```
npm install --global nrm
nrm test
nrm ls
nrm use cnpm

// 推荐使用cnpm部署私有源镜像服务器
nrm add yourcompany http://registry.npm.yourcompany.com/
```



### 源码编译node

```
sudo apt-get install g++ curl libssl-dev apache2-utils git-core build-essential

git clone https://github.com/nodejs/node.git
cd node
./configure
make
sudo make install
```




