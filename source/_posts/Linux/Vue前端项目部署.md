# Vue前端项目部署

1. 编辑前端项目配置文件vue.config.js

   ```javascript
   module.exports = {
       //公共访问路径,和nginx配置有关
       publicPath: '/',
       devServer: {
           port: 前端服务端口,
           // 设置代理, 该proxy属性是后端主机的地址,可域名也可https
           proxy:{
               '/api':{
                   //后端项目运行的 http://ip:端口号
                   target: 'http://后端服务器:后端服务端口',
                   //跨域,若不允许跨域则要求前后端端口必须一致
                   changeOrigin: true,
                   ws: true,
                   //地址重写
                   pathRewrite: {
                       '^/api': ''
                   }
               }
           }
       },
     }
   ```

   与nginx相关的介绍,参考网址:[手把手教 Nginx 部署 Vue 项目 - 掘金 (juejin.cn)](https://juejin.cn/post/6844904096973979662)

2. 通过`npm run build`指令,将前端项目打包

   > 本质上执行的是`vue-cli-service build`

   打包完成后将在项目根目录生成dist目录,将dist目录移至云服务器上,路径可以自定义,但是要记住位置

3. 云服务器上安装nginx,这里以Ubuntu 20.04LTS为例:

   `sudo apt install nginx`

4. 然后找到nginx的配置文件`nginx.conf`,一般在`/etc/nginx`目录下,如果没有,也可以通过`whereis nginx`命令找到nginx相关的目录,然后找到配置文件

5. 修改配置文件,这里只截取了要配置的部分,一般`http{}`部分是存在的,但是`server{}`部分是需要自己写入的:

   ```conf
   http {
   	server {
   		listen <前端服务端口>;
   		server_name <服务器ip>;
   		location / {
   			# root后面是打包后dist目录的路径
   			root /var/project/front/dist;
   			# 默认访问页面
   			try_files $uri $uri/ /index.html;
   			index index.html index.htm;
   			proxy_method POST;
   			# 指定错误代码
   			error_page 405 =200 /index.html;
   		}
   		location ^~ /api/ {
   			proxy_pass http://<后端服务ip>:<后端服务端口>/;
   		}
   	}
   }
   ```

6. 修改完成后,通过`nginx -s reload`命令应用配置

7. 然后在浏览器访问`http://<服务器ip>:<前端端口>`,即可访问到前端项目

7. 如果有路径不对的注意修改main.js、vue.config.js、upload.vue的路径