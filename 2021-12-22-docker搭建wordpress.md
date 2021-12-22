### docker启动服务

1. **拉取mysql和wordpress镜像**

   `dokcer pull mysql:8.0.18`

   `docker pull wordpress`

2. **启动mysql容器**

   `docker run -itd --name wp_mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=111111 mysql:8.0.18`

3. **给wordpress创建访问mysql的用户**

   * 首先进入mysql容器内部

     `docker exec -it wp_mysql /bin/bash`

   * 进入mysql

     `mysql -u root -p`

   * 创建wordpress数据库

     `create database wordpress character set UTF8 collate utf8_bin;`

   * 创建wordpress的用户

     `CREATE USER 'wordpress_user'@'%' IDENTIFIED BY '111111';`

   * 赋权限

     `GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpress_user'@'%';`

   * 应用权限

     `flush privileges;`

4. **启动wordpress容器**

   `docker run --name wordpress -p 8080:80 -d wordpress`

### 配置wordpress

1. 设置语言

   ![image-20211222112539133](C:\Users\jeremy\AppData\Roaming\Typora\typora-user-images\image-20211222112539133.png)

2. 设置数据库

   ![image-20211222112731556](C:\Users\jeremy\AppData\Roaming\Typora\typora-user-images\image-20211222112731556.png)

3. 设置wordpress站点账号密码，然后访问ip:8080即可访问