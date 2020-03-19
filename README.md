# 使用docker-compose以ws+tls方式快速部署科学上网利器v2ray


## 更新日志

* 2020年3月3日：增加v2ray并使用ws+tls方式实现代理服务；
* 2020年3月1日：增加nginx服务并启用certbot证书；

## 使用步骤

1. 获取域名及VPS

* 免费域名注册： <a href="https://www.freenom.com/zh/index.html?lang=zh" target="_blank">免费域名申请</a>；；
* VPS推荐搬瓦工，支持支付宝付款： <a href="https://www.4spaces.org/best-details-to-buy-banwagonhost/" target="_blank">史上最详细搬瓦工VPS注册/购买图文教程(内附优惠券)</a>

2. 安装docker-ce并启动

* 安装

```
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
```

* 添加用户到用户组

```
sudo gpasswd -a $USER docker
```

* 启动

```
systemctl start docker
```

3. 安装`docker-compose`

```
$  sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

$ sudo chmod +x /usr/local/bin/docker-compose

$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

4. 修改v2ray配置

**1) `init-letsencrypt.sh`**

将里面的`domains`和`email`修改为自己的域名和邮箱。

**2) `docker-compose.yml`**

可以不用动。

**3) `data/v2ray/config.json`**

修改ID，`"id": "bae399d4-13a4-46a3-b144-4af2c0004c2e"`，也可以不修改。

**4) `data/nginx/conf.d/v2020_v2ray.conf`**

修改所有`your_domain`为自己的域名，其他地方，如果上面可以修改的地方你没修改，那么除了域名之外的也不用修改了。

5. 一键部署v2ray

```
chomod +x ./init-letsencrypt.sh

sudo ./init-letsencrypt.sh
```

6. 进行v2ray客户端配置

细节参考： <a href="https://www.4spaces.org/docker-compose-install-v2ray-ws-tls/" target="_blank" rel="noopener noreferrer">在docker-compose环境下以ws+tls方式搭建v2ray(So easy)</a>