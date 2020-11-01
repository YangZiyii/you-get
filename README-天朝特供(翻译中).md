# You-Get 天朝特供（翻译中）



**注意事项:如果您正在寻找传统的“问题”选项卡，请阅读[此内容](https://github.com/soimort/you-get/blob/develop/CONTRIBUTING.md)**

---

[You-Get](https://you-get.org/) 是一个用来下载网上的媒体文件(视频,音频, 图片)的小命令行实用程序, 以防网站莫得下载的方法

这是用 `you-get` 下载 [油管](https://www.youtube.com/watch?v=jNQXAC9IVRw)视频的方法:

```console
$ you-get 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
site:                YouTube
title:               Me at the zoo
stream:
    - itag:          43
      container:     webm
      quality:       medium
      size:          0.5 MiB (564215 bytes)
    # download-with: you-get --itag=43 [URL]

Downloading Me at the zoo.webm ...
 100% (  0.5/  0.5MB) ├██████████████████████████████████┤[1/1]    6 MB/s

Saving Me at the zoo.en.srt ... Done.
```

你可能会因为如下理由使用它:

* 你发现了网上的好玩的东西,而且你选择下载一份
* 你看到了一个逗比视频,但是网站不让你下载。你想，“劳资自个的电脑还造反了！！！” (明显不是滋油的网络该有的样子)
* 你想摆脱万恶的闭源软件的污秽和保护性的JavaScript代码, 而且不想让Flash玷污了你神圣的AIPC。
* 你是黑阔精神和自由软件的化身

 `you-get` 能嘎哈:

* 从 油管,优酷, Niconico之类的热门网站下载视频、音频。 (不止这仨，还有 [ 这些](#supported-sites))
* 用自己的播放器看网上的视频，摆脱浏览器和广告
* 通过抓取网页下载感兴趣的图片。
* 下载任意非HTML内容，即二进制文件。

心动了咩? 那就现在赶紧[下载](#installation)吧！and [get started by examples](#getting-started).

你系Python程序猿咩? 那还不赶紧fork一份[源码](https://github.com/soimort/you-get)!

![](https://i.imgur.com/GfthFAz.png)

## Installation

### Prerequisites

The following dependencies are necessary:

* **[Python](https://www.python.org/downloads/)**  3.2 or above
* **[FFmpeg](https://www.ffmpeg.org/)** 1.0 or above
* (Optional) [RTMPDump](https://rtmpdump.mplayerhq.hu/)

### Option 1: Install via pip

The official release of `you-get` is distributed on [PyPI](https://pypi.python.org/pypi/you-get), and can be installed easily from a PyPI mirror via the [pip](https://en.wikipedia.org/wiki/Pip_\(package_manager\)) package manager. Note that you must use the Python 3 version of `pip`:

    $ pip3 install you-get

### Option 2: Install via [Antigen](https://github.com/zsh-users/antigen) (for Zsh users)

Add the following line to your `.zshrc`:

    antigen bundle soimort/you-get

### Option 3: Download from GitHub

You may either download the [stable](https://github.com/soimort/you-get/archive/master.zip) (identical with the latest release on PyPI) or the [develop](https://github.com/soimort/you-get/archive/develop.zip) (more hotfixes, unstable features) branch of `you-get`. Unzip it, and put the directory containing the `you-get` script into your `PATH`.

Alternatively, run

```
$ [sudo] python3 setup.py install
```

Or

```
$ python3 setup.py install --user
```

to install `you-get` to a permanent path.

### Option 4: Git clone

This is the recommended way for all developers, even if you don't often code in Python.

```
$ git clone git://github.com/soimort/you-get.git
```

Then put the cloned directory into your `PATH`, or run `./setup.py install` to install `you-get` to a permanent path.

### Option 5: Homebrew (Mac only)

You can install `you-get` easily via:

```
$ brew install you-get
```

### Option 6: pkg (FreeBSD only)

You can install `you-get` easily via:

```
# pkg install you-get
```

### Shell completion

Completion definitions for Bash, Fish and Zsh can be found in [`contrib/completion`](https://github.com/soimort/you-get/tree/develop/contrib/completion). Please consult your shell's manual for how to take advantage of them.

## Upgrading

Based on which option you chose to install `you-get`, you may upgrade it via:

```
$ pip3 install --upgrade you-get
```

or download the latest release via:

```
$ you-get https://github.com/soimort/you-get/archive/master.zip
```

In order to get the latest ```develop``` branch without messing up the PIP, you can try:

```
$ pip3 install --upgrade git+https://github.com/soimort/you-get@develop
```

## 开始

### 下载视频

When you get a video of interest, you might want to use the `--info`/`-i` option to see all available quality and formats:

```
$ you-get -i 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
site:                YouTube
title:               Me at the zoo
streams:             # Available quality and codecs
    [ DASH ] ____________________________________
    - itag:          242
      container:     webm
      quality:       320x240
      size:          0.6 MiB (618358 bytes)
    # download-with: you-get --itag=242 [URL]

    - itag:          395
      container:     mp4
      quality:       320x240
      size:          0.5 MiB (550743 bytes)
    # download-with: you-get --itag=395 [URL]

    - itag:          133
      container:     mp4
      quality:       320x240
      size:          0.5 MiB (498558 bytes)
    # download-with: you-get --itag=133 [URL]

    - itag:          278
      container:     webm
      quality:       192x144
      size:          0.4 MiB (392857 bytes)
    # download-with: you-get --itag=278 [URL]

    - itag:          160
      container:     mp4
      quality:       192x144
      size:          0.4 MiB (370882 bytes)
    # download-with: you-get --itag=160 [URL]

    - itag:          394
      container:     mp4
      quality:       192x144
      size:          0.4 MiB (367261 bytes)
    # download-with: you-get --itag=394 [URL]

    [ DEFAULT ] _________________________________
    - itag:          43
      container:     webm
      quality:       medium
      size:          0.5 MiB (568748 bytes)
    # download-with: you-get --itag=43 [URL]

    - itag:          18
      container:     mp4
      quality:       small
    # download-with: you-get --itag=18 [URL]

    - itag:          36
      container:     3gp
      quality:       small
    # download-with: you-get --itag=36 [URL]

    - itag:          17
      container:     3gp
      quality:       small
    # download-with: you-get --itag=17 [URL]
```

By default, the one on the top is the one you will get. If that looks cool to you, download it:

```
$ you-get 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
site:                YouTube
title:               Me at the zoo
stream:
    - itag:          242
      container:     webm
      quality:       320x240
      size:          0.6 MiB (618358 bytes)
    # download-with: you-get --itag=242 [URL]

Downloading Me at the zoo.webm ...
 100% (  0.6/  0.6MB) ├██████████████████████████████████████████████████████████████████████████████┤[2/2]    2 MB/s
Merging video parts... Merged into Me at the zoo.webm

Saving Me at the zoo.en.srt ... Done.
```

(If a YouTube video has any closed captions, they will be downloaded together with the video file, in SubRip subtitle format.)

Or, if you prefer another format (mp4), just use whatever the option `you-get` shows to you:

```
$ you-get --itag=18 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
```

**提示:**

* At this point, format selection has not been generally implemented for most of our supported sites; in that case, the default format to download is the one with the highest quality.
* `ffmpeg` is a required dependency, for downloading and joining videos streamed in multiple parts (e.g. on some sites like Youku), and for YouTube videos of 1080p or high resolution.
* If you don't want `you-get` to join video parts after downloading them, use the `--no-merge`/`-n` option.

### 下载其他东西

如果你已经有你想要的东西的URL了,你可以直接:

```
$ you-get https://stallman.org/rms.jpg
Site:       stallman.org
Title:      rms
Type:       JPEG Image (image/jpeg)
Size:       0.06 MiB (66482 Bytes)

Downloading rms.jpg ...
100.0% (  0.1/0.1  MB) ├████████████████████████████████████████┤[1/1]  127 kB/s
```

Otherwise, `you-get` will scrape the web page and try to figure out if there's anything interesting to you:

```
$ you-get http://kopasas.tumblr.com/post/69361932517
Site:       Tumblr.com
Title:      kopasas
Type:       Unknown type (None)
Size:       0.51 MiB (536583 Bytes)

Site:       Tumblr.com
Title:      tumblr_mxhg13jx4n1sftq6do1_1280
Type:       Portable Network Graphics (image/png)
Size:       0.51 MiB (536583 Bytes)

Downloading tumblr_mxhg13jx4n1sftq6do1_1280.png ...
100.0% (  0.5/0.5  MB) ├████████████████████████████████████████┤[1/1]   22 MB/s
```

**提示:**

* This feature is an experimental one and far from perfect. It works best on scraping large-sized images from popular websites like Tumblr and Blogger, but there is really no universal pattern that can apply to any site on the Internet.

### 在 Google Videos 上搜索并下载一个视频

 `you-get`是万能的. 哪怕你给的关键词连个URL都不是, `you-get`仍然会在谷歌上搜一个相关的最热门的视频 (哪怕不一定是你想看的视频，起码也差不多)

```
$ you-get "蓝蓝路"
```

### Pause and resume a download

You may use <kbd>Ctrl</kbd>+<kbd>C</kbd> to interrupt a download.

A temporary `.download` file is kept in the output directory. Next time you run `you-get` with the same arguments, the download progress will resume from the last session. In case the file is completely downloaded (the temporary `.download` extension is gone), `you-get` will just skip the download.

To enforce re-downloading, use the `--force`/`-f` option. (**Warning:** doing so will overwrite any existing file or temporary file with the same name!)

### Set the path and name of downloaded file

Use the `--output-dir`/`-o` option to set the path, and `--output-filename`/`-O` to set the name of the downloaded file:

```
$ you-get -o ~/Videos -O zoo.webm 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
```

**小技巧:**

* These options are helpful if you encounter problems with the default video titles, which may contain special characters that do not play well with your current shell / operating system / filesystem.
* These options are also helpful if you write a script to batch download files and put them into designated folders with designated names.

### Proxy settings

You may specify an HTTP proxy for `you-get` to use, via the `--http-proxy`/`-x` option:

```
$ you-get -x 127.0.0.1:8087 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
```

However, the system proxy setting (i.e. the environment variable `http_proxy`) is applied by default. To disable any proxy, use the `--no-proxy` option.

**小技巧:**

* 如果你经常需要用代理服务器上网(以防你那里某些网站被墙了), you might want to use `you-get` with [proxychains](https://github.com/rofl0r/proxychains-ng) and set `alias you-get="proxychains -q you-get"` (in Bash).
* 像优酷这样只有你身在天朝（不包含港澳台特别行政区）才能够访问的网站, there is an option of using a specific proxy to extract video information from the site: `--extractor-proxy`/`-y`.

### 看视频

Use the `--player`/`-p` option to feed the video into your media player of choice, e.g. `mpv` or `vlc`, instead of downloading it:

```
$ you-get -p vlc 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
```

Or, if you prefer to watch the video in a browser, just without ads or comment section:

```
$ you-get -p chromium 'https://www.youtube.com/watch?v=jNQXAC9IVRw'
```

**小技巧:**

* It is possible to use the `-p` option to start another download manager, e.g., `you-get -p uget-gtk 'https://www.youtube.com/watch?v=jNQXAC9IVRw'`, though they may not play together very well.

### Load cookies

Not all videos are publicly available to anyone. If you need to log in your account to access something (e.g., a private video), it would be unavoidable to feed the browser cookies to `you-get` via the `--cookies`/`-c` option.

**提醒:**

* As of now, we are supporting two formats of browser cookies: Mozilla `cookies.sqlite` and Netscape `cookies.txt`.

####  **重用提取的数据** 

 使用```-url`/-u```可获取从页面提取的可下载资源url的列表。使用```-json```以json格式获取提取数据的摘要。 

**警告:**

* For the time being, this feature has **NOT** been stabilized and the JSON schema may have breaking changes in the future.

## Supported Sites

|                Site                 |                            URL                            | Videos? | Images? | Audios? |
| :---------------------------------: | :-------------------------------------------------------: | :-----: | :-----: | :-----: |
|             **YouTube**             |                <https://www.youtube.com/>                 |    ✓    |         |         |
|             **Twitter**             |                  <https://twitter.com/>                   |    ✓    |    ✓    |         |
|                 VK                  |                     <http://vk.com/>                      |    ✓    |    ✓    |         |
|                Vine                 |                    <https://vine.co/>                     |    ✓    |         |         |
|                Vimeo                |                   <https://vimeo.com/>                    |    ✓    |         |         |
|                Veoh                 |                  <http://www.veoh.com/>                   |    ✓    |         |         |
|             **Tumblr**              |                 <https://www.tumblr.com/>                 |    ✓    |    ✓    |    ✓    |
|                 TED                 |                   <http://www.ted.com/>                   |    ✓    |         |         |
|             SoundCloud              |                 <https://soundcloud.com/>                 |         |         |    ✓    |
|              SHOWROOM               |             <https://www.showroom-live.com/>              |    ✓    |         |         |
|              Pinterest              |               <https://www.pinterest.com/>                |         |    ✓    |         |
|                MTV81                |                  <http://www.mtv81.com/>                  |    ✓    |         |         |
|              Mixcloud               |                <https://www.mixcloud.com/>                |         |         |    ✓    |
|              Metacafe               |                <http://www.metacafe.com/>                 |    ✓    |         |         |
|               Magisto               |                 <http://www.magisto.com/>                 |    ✓    |         |         |
|            Khan Academy             |              <https://www.khanacademy.org/>               |    ✓    |         |         |
|          Internet Archive           |                  <https://archive.org/>                   |    ✓    |         |         |
|            **Instagram**            |                 <https://instagram.com/>                  |    ✓    |    ✓    |         |
|                InfoQ                |           <http://www.infoq.com/presentations/>           |    ✓    |         |         |
|                Imgur                |                    <http://imgur.com/>                    |         |    ✓    |         |
|         Heavy Music Archive         |               <http://www.heavy-music.ru/>                |         |         |    ✓    |
|              Freesound              |                <http://www.freesound.org/>                |         |         |    ✓    |
|               Flickr                |                 <https://www.flickr.com/>                 |    ✓    |    ✓    |         |
|              FC2 Video              |                  <http://video.fc2.com/>                  |    ✓    |         |         |
|              Facebook               |                <https://www.facebook.com/>                |    ✓    |         |         |
|                eHow                 |                  <http://www.ehow.com/>                   |    ✓    |         |         |
|             Dailymotion             |               <http://www.dailymotion.com/>               |    ✓    |         |         |
|                Coub                 |                    <http://coub.com/>                     |    ✓    |         |         |
|                 CBS                 |                   <http://www.cbs.com/>                   |    ✓    |         |         |
|              Bandcamp               |                  <http://bandcamp.com/>                   |         |         |    ✓    |
|              AliveThai              |                   <http://alive.in.th/>                   |    ✓    |         |         |
|             interest.me             |                <http://ch.interest.me/tvn>                |    ✓    |         |         |
|      **755<br/>ナナゴーゴー**       |                    <http://7gogo.jp/>                     |    ✓    |    ✓    |         |
|    **niconico<br/>ニコニコ動画**    |                <http://www.nicovideo.jp/>                 |    ✓    |         |         |
| **163<br/>网易视频<br/>网易云音乐** |      <http://v.163.com/><br/><http://music.163.com/>      |    ✓    |         |    ✓    |
|                56网                 |                   <http://www.56.com/>                    |    ✓    |         |         |
|              **AcFun**              |                  <http://www.acfun.cn/>                   |    ✓    |         |         |
|       **Baidu<br/>百度贴吧**        |                 <http://tieba.baidu.com/>                 |    ✓    |    ✓    |         |
|              爆米花网               |                <http://www.baomihua.com/>                 |    ✓    |         |         |
|      **bilibili<br/>哔哩哔哩**      |                <http://www.bilibili.com/>                 |    ✓    |    ✓    |    ✓    |
|                豆瓣                 |                 <http://www.douban.com/>                  |    ✓    |         |    ✓    |
|                斗鱼                 |                 <http://www.douyutv.com/>                 |    ✓    |         |         |
|              凤凰视频               |                   <http://v.ifeng.com/>                   |    ✓    |         |         |
|               风行网                |                   <http://www.fun.tv/>                    |    ✓    |         |         |
|          iQIYI<br/>爱奇艺           |                  <http://www.iqiyi.com/>                  |    ✓    |         |         |
|               激动网                |                   <http://www.joy.cn/>                    |    ✓    |         |         |
|                酷6网                |                   <http://www.ku6.com/>                   |    ✓    |         |         |
|              酷狗音乐               |                  <http://www.kugou.com/>                  |         |         |    ✓    |
|              酷我音乐               |                   <http://www.kuwo.cn/>                   |         |         |    ✓    |
|               乐视网                |                   <http://www.le.com/>                    |    ✓    |         |         |
|               荔枝FM                |                  <http://www.lizhi.fm/>                   |         |         |    ✓    |
|                秒拍                 |                 <http://www.miaopai.com/>                 |    ✓    |         |         |
|            MioMio弹幕网             |                  <http://www.miomio.tv/>                  |    ✓    |         |         |
|         MissEvan<br/>猫耳FM         |                <http://www.missevan.com/>                 |         |         |    ✓    |
|               痞客邦                |                 <https://www.pixnet.net/>                 |    ✓    |         |         |
|              PPTV聚力               |                  <http://www.pptv.com/>                   |    ✓    |         |         |
|               齐鲁网                |                   <http://v.iqilu.com/>                   |    ✓    |         |         |
|           QQ<br/>腾讯视频           |                    <http://v.qq.com/>                     |    ✓    |         |         |
|              企鹅直播               |                   <http://live.qq.com/>                   |    ✓    |         |         |
| Sina<br/>新浪视频<br/>微博秒拍视频  | <http://video.sina.com.cn/><br/><http://video.weibo.com/> |    ✓    |         |         |
|          Sohu<br/>搜狐视频          |                   <http://tv.sohu.com/>                   |    ✓    |         |         |
|         **Tudou<br/>土豆**          |                  <http://www.tudou.com/>                  |    ✓    |         |         |
|                虾米                 |                  <http://www.xiami.com/>                  |    ✓    |         |    ✓    |
|              阳光卫视               |                 <http://www.isuntv.com/>                  |    ✓    |         |         |
|             **音悦Tai**             |                <http://www.yinyuetai.com/>                |    ✓    |         |         |
|         **Youku<br/>优酷**          |                  <http://www.youku.com/>                  |    ✓    |         |         |
|               战旗TV                |               <http://www.zhanqi.tv/lives>                |    ✓    |         |         |
|               央视网                |                   <http://www.cntv.cn/>                   |    ✓    |         |         |
|          Naver<br/>네이버           |                <http://tvcast.naver.com/>                 |    ✓    |         |         |
|               芒果TV                |                  <http://www.mgtv.com/>                   |    ✓    |         |         |
|               火猫TV                |                 <http://www.huomao.com/>                  |    ✓    |         |         |
|             阳光宽频网              |                  <http://www.365yg.com/>                  |    ✓    |         |         |
|              西瓜视频               |                 <https://www.ixigua.com/>                 |    ✓    |         |         |
|               新片场                |             <https://www.xinpianchang.com//>              |    ✓    |         |         |
|                快手                 |                <https://www.kuaishou.com/>                |    ✓    |    ✓    |         |
|                抖音                 |                 <https://www.douyin.com/>                 |    ✓    |         |         |
|               TikTok                |                 <https://www.tiktok.com/>                 |    ✓    |         |         |
|            中国体育(TV)             |    <http://v.zhibo.tv/> </br><http://video.zhibo.tv/>     |    ✓    |         |         |
|                知乎                 |                 <https://www.zhihu.com/>                  |    ✓    |         |         |

 对于列表中没有的所有其他站点，UniversalExtractor将负责从页面中查找和下载有趣的资源。 

### 那些已知的bug

如果啥东西出毛病了导致 `you-get` 弄不到你想要的东西,不要慌 (是的，这经常发生，莫样咧？)

在 <https://github.com/soimort/you-get/wiki/Known-Bugs>查一下这是不是个已知的问题.如果不是的话，  [请汇报问题](https://github.com/soimort/you-get/blob/develop/CONTRIBUTING.md)。

##  参与其中 

你可以通过Gitter频道联系我们(https://gitter.im/soimert/you-get)（以下是您如何为Gitter[设置IRC客户端](http://irc.gitter.im)）。如果你有一个关于`you-get`”的问题，可以在那里问。 



 如果您想报告问题或投稿，请务必首先阅读[指南](https://github.com/soimert/you-get/blob/develop/contribution.md)。 

## 法律问题

代码用 [MIT license](https://raw.github.com/soimort/you-get/master/LICENSE.txt) 开源。

请注意一件特殊的事，

> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
> IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
> FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
> AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
> LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
> OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
> SOFTWARE.

用人话讲，就是:

 *如果您使用本软件构成侵犯版权的依据，或您将本软件用于任何其他非法目的，作者不承担任何责任* 

**我就把代码搁这儿,你打算嘎哈不关劳资屁事** 

## 作者

此软件由[@soimort](https://github.com/soimort)制作, 一个由:coffee:, :beer: 和 :ramen:续命的人

 您可以在这里找到[所有贡献者列表](https://github.com/soimert/you-get/graphs/contributors)。 
