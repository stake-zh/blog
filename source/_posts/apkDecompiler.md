title: "apkDecompiler"
date: 2015-05-08 18:25:16
tags: android 
---
需要准备工具(基于mac环境) 
>1. apktool <http://ibotpeaches.github.io/Apktool/>
>2. jd-gui <http://jd.benow.ca/>
>3. dex2jar <http://sourceforge.net/projects/dex2jar/>


## apktool
作用：
>生成apk的资源文件

步骤：
>1. terminal进入apktool目录
>2. 运行 `java -jar apktool.jar d target.apk `，会生成target文件夹

## dex2jar
作用
>生成jd-gui可读的jar包

步骤：
>1. 修改apk后缀为zip
>2. 将zip中classes.dex文件到dex2jar文件中
>3. 运行 `./d2j-dex2jar.sh classes.dex`

##ju-gui
打开app后，找到刚才生成的classes-dex2jar.jar 即可
