title: "set font size of gitk on retina  mac book pro"
date: 2015-05-19 20:22:37
tags: device
---

## 在rmcp 中修改gitk字体

gitk、citool在高分辨率的macbook pro上看起来像素画特别严重，很不方便使用。通过查下一些资料发现方法，比如在 

* [Super User](http://superuser.com/questions/620824/is-it-possible-to-have-git-gui-gitk-look-good-on-a-retina-macbook-pro)的提问，但是对我不适应。
* 在上边连接中还有一个方法就是使用一个降低分辨率的软件[retinizer](https://sites.google.com/a/mikelpr.com/retinizer/)，这是一个多么邪恶的想法。
* 方向这样一个网址[Making gitk look sexy on Mac OS X](http://effectif.com/git/making-gitk-look-good-on-mac)但是很不幸，这还还是对我不适用。但是在评论中发现了我使用的简单易用的方法。

其实有这样一个文件，在`~/.config/git/gitk`中有gitk的配置文件，我们可以在里面修改字体。只需要配修改前三行的字体即可：

```
set mainfont {{Lucida Grande} 14}
set textfont {Monaco 14}
set uifont {{Lucida Grande} 12 bold}
```

这时候再打开gitk和citool，世界终于安静了

---

gitk looks really pixelated and ugly on the retina macbook. It`s very unconvenient to look. After the google, i found some solutions.

* the solution in web [Super User](http://superuser.com/questions/620824/is-it-possible-to-have-git-gui-gitk-look-good-on-a-retina-macbook-pro), but unfortunately, this not fit for me.
* another solution in this webpage is low dow DPI with the app of [retinizer](https://sites.google.com/a/mikelpr.com/retinizer/). What a pity idea!
* in the webpage of [Making gitk look sexy on Mac OS X](http://effectif.com/git/making-gitk-look-good-on-mac),that mention a way to improve the visual, but that method still not work for me. In the commments of this article, i found some very nice way.

In fact, there is config file in`~/.config/git/gitk`,just vim the file and reset the font size. It just modify the front three line of the file.

```
set mainfont {{Lucida Grande} 14}
set textfont {Monaco 14}
set uifont {{Lucida Grande} 12 bold}
```
Now open the gitk or citool, world peace at last.