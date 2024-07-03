
# 参考
[MacOS(M1)下创建Docker Ubuntu容器搭建CSAPP实验环境并运行](https://blog.csdn.net/weixin_52693116/article/details/133149517)

# 踩坑
Docker下载安装，官网访问不了。可以在这[下载地址](https://www.macw.com/mac/3356.html?id=Mjg0ODY4Jl8mMjcuMTg3LjIyNC4xMTI%3D&continueFlag=34612167169c183d5c4be110f99e38b1)


Docker镜像
在docker desktop右上角 设置图标-Docker Engine 里 用以下代码替换文本框内容
```json
{
  "experimental": false,
  "registry-mirrors": [
    //这个失效了，到阿里云镜像服务搞
    "https://docker.mirrors.ustc.edu.cn" 
  ],
  "features": {
    "buildkit": true
  }
}
```
镜像地址，到[阿里云容器镜像服务](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)搞一个,替换上面的`https://docker.mirrors.ustc.edu.cn`

开发工具  可以用clion

Docker容器关闭后
```
打开Docker desktop
docker container start csapp_env
```

