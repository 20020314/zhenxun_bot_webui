# 开发环境使用方式（请先进入webui根目录文件夹下再使用命令）

****

### 开发环境用于修改和测试源码，启动开发服务会占用一定的资源和性能
### 开发环境需要下载nodejs，未安装请移步链接 https://nodejs.org/zh-cn/download/



## 使用npm（nodejs自带）

### 下载webui开发依赖

```
npm install
```

### 启动开发服务
```
npm run serve
```

### 打包生产环境资源
```
npm run build
```

## 使用yarn（需要下载）

### 使用npm安装yarn

```
npm install --global yarn
```

### 下载webui开发依赖

```
yarn install
```

### 启动开发服务
```
yarn serve
```

### 打包生产环境资源
```
yarn build
```
****






## 更新

### 2022/6/20 \[v0.1.0.4] 
* 优化普通插件列表在低宽度屏幕下的体验

### 2022/6/18

* 修复cookie储存异常的问题
* 侧边栏在低分辨率屏幕下自动隐藏

### 2022/6/5 \[v0.1.0.3] (__务必使用zhenxun_bot_v0.1.5.9及以上版本！！！__)
* 新增修改“webui请求api地址”的页面以及功能
* 接口数据类型对齐zhenxun_bot_v0.1.5.9
* 样式体验优化，移动端下样式优化

### 2022/5/31

* 样式表现优化
* 主界面移动端简易简易适配


### 2022/5/28

* 修复配置项和编辑项某些情况下修改出错的问题
* 改变用户身份信息储存方式，7天内可以免登陆
* 部分样式表现优化
* 控制台警告处理
