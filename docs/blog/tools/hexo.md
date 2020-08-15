
## hexo踩坑

### 创建新的文章 
```
1. hexo new post “博客名”
2. hexo g
3. hexo s  //开启服务
4. 如端口被占用  hexo server -p 端口号 修改端口号
5. hexo d -g 推送部署上线
```

[参考链接](https://www.jianshu.com/p/4f56cf990bba)


### 404解决方法
 - 观察是否使用http，换为https访问即可

### 查看node安装位置
 - `window` 使用 where node 
 - `mac`   使用 which node