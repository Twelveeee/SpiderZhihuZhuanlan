https://zhuanlan.zhihu.com/xueAI 的爬虫

# 知乎人工智能学习专栏 python爬虫

功能是将知乎专栏的文章爬下来，变成docx文件。

## 1.获取专栏的URL

自动获取，获取后url存在`homePath+"cache\\urlListCache.json`里面，每次执行程序会自动对比最新十条，是否有重复的链接。如果有就停止继续获取，否则获取到完。

## 2.生成DOC文件

根据专栏的URL生成doc文件，用python docx。
自动写入标题和作者 
如果出现代码块，文件中会出现`【CODE】`需要自己手动截图。
如果出现的图片太小，会自动用哔哩哔哩的logo代替（不要问我为什么）
有的时候列表会合成变成一行文字，到时候再注意。
如果出现图片有小字部分，文件中会出现"【"+小字部分的内容+"】"，需要手动高亮。

命名的时候，如果作者是“逆暗”、“裴丘”、“hooo”，则在文件名字最前面加上"【#】"。

## 3.人工审核

生成的docx文件名没有加日期，需要人工对比一下文章，然后手动加一下日期，怕出错。

文章里面，搜索一下“【”就能看到哪里需要手动改

## 4.第一次使用时的配置

直接在vscode里面运行吧。
导入

```python
import requests
import re
from bs4 import BeautifulSoup
import os
import urllib
from docx import Document
from docx.shared import RGBColor
from docx.oxml.ns import qn
from docx.shared import Pt
import time
import json
```

看看缺哪个弄哪个。

```python
#定义常量
homePath = "D:\\Work\\Document\\BaiduZhihu\\" #家目录 
docPath = homePath+"发送缓存区\\" #生成的DOC文件出现在哪里
imgCache = homePath+"cache\\imgcache.jpg" #图片缓存位置
logPath = homePath+"cache\\log.txt" #log位置不用管
log2Path =homePath+"发送缓存区\\[log].txt" #一共弄了什么文件，log

```

如果要改成爬其他专栏的话，需要修改

```python
urlList = getXueAI("这部分")
```

打开需要爬的专栏页面，此时按F12键，点Network，然后把页面往下滑，会发现网页发起了个请求，其中一个以articles开头的会看到里面的Request URL如下：

```python
https://zhuanlan.zhihu.com/api/columns/xueAI/articles?include=data%5B*%5D.admin_closed_comment%2Ccomment_count%2Csuggest_edit%2Cis_title_image_full_screen%2Ccan_comment%2Cupvoted_followees%2Ccan_open_tipjar%2Ccan_tip%2Cvoteup_count%2Cvoting%2Ctopics%2Creview_info%2Cauthor.is_following%2Cis_labeled%2Clabel_info
```

貌似没有什么需要添加的了。就这酱。

