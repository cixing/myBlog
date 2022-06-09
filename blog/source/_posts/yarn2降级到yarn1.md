---
title: yarn2降级到yarn1
date: 2022-06-09 15:31:43
tags: 前端 yarn monorepo
---
## yarn2降级到yarn1失败
### 起因

yarn install在流水线中，会安装所有的项目依赖。 如果只想打包一个项目依赖， yarn 1的workspace不支持，需要升级到yarn2

#### 如何安装yarn2
``` bash
npm i yarn -g
yarn set version berry
```
然后发现升级到了 3.2.1


``` bash
yarn workspaces focus --production XXX（子项目包名）
```
只安装了子项目下的依赖，跟目录依赖没有安装

这个问题现在还没解决

由于项目需要yarn 1 于是降级 yarn2 发现怎么都安装不了yarn1， 哪怕卸载了yarn 又安装，默认就变成了 yarn 3.2.1 

### 降级yarn2

https://github.com/yarnpkg/berry/issues/999

查看yarn berry issue后解决

``` bash
cat ~/.yarnrc.yml 
> yarnPath: ".yarn/releases/yarn-berry.cjs"

rm -f ~/.yarnrc.yml

npm install -g 'yarn@1.22.1'

yarn -v
> 1.22.10
```
