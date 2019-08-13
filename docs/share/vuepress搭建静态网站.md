# vuepress搭建静态网站

-  全局安装vuepress
> npm install -g vuepress

-  初始化项目
> npm init -y

-  新建docs文件夹
docs文件夹作为项目文档根目录，主要放置Markdown类型的文章和.vuepress文件夹。
> mkdir docs

-  设置package.json  
VuePress中有两个命令:  
vuepress dev docs命令运行本地服务，通过访问http://localhost:8080即可预览网站;  
vuepress build docs命令用来生成静态文件，默认情况下，放置在docs/.vuepress/dist目录中;  
当然可以在docs/.vuepress/config.js中的dest字段来修改默认存放目录。  
在这里将两个命令封装成脚本的方式，直接使用npm run dev和npm run build即可
```
{
  "scripts": {
    "dev": "vuepress dev docs",
    "build": "vuepress build docs"
  }
}
```

-  创建.vuepress目录
在docs目录中，创建.vuepress目录，.vuepress目录主要用于存放VuePress相关的文件。

-  创建config.js
进入到.vuepress目录中，然后创建config.js，config.js是VuePress必要的配置文件
config.js的主要配置包括网站的标题、描述等基本信息，以及主题的配置
-  创建public文件夹
进入到.vuepress目录中，然后创建public文件夹，此文件夹主要放静态资源文件，例如favicons和 PWA的图标。
