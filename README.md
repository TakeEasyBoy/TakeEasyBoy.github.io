# TakeEasyBoy.github.io
_post下的md文件,需要使用yyyy-mm-dd-name.md的格式书写,否则列表不会被渲染;因为jekyll在生成路径的时候回将其生成为yyyy/mm/dd/name.html的格式

> 安装 [install ruby](https://rubyinstaller.org/downloads/)
> 安装**jekyll**,命令行中执行:  ```gem install jekyll bundler```
> ```bundle install && bundle exec jekyll serve``` 浏览器中查看 0.0.0.0:4000

## environment JEKYLL_ENV=production bundle exec jekyll build
该功能可以用来实现一些在pro环境下的脚本引入
```
{% if jekyll.environment == "production" %}
  <script src="my-analytics-script.js"></script>
{% endif %}
```