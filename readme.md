# win实现xiaoaiGPT

你可以在[notion](https://circular-kettle-026.notion.site/win-xiaoaiGPT-86105dd6757e47988bca58cca21d6bdc)上看到视频演示。

**特别说明，这是一个很有趣的玩具，不要有太高期待，目前没有太大生产力价值，不仅是网络延迟问题，更重要是小爱的语音转文字错别字太多了，尤其是英语。。。**

准备：

1. ChatGPT id
2. 小爱音响
3. 能正常联网的环境或 proxy
4. python3.8+

xiaoaiGPT是github上一位大佬[yihong0618](https://github.com/yihong0618/xiaogpt/commits?author=yihong0618)开发出来的，截止至2023-3-17-0：34，大佬还没补充win实现步骤，我迫不及待在自己电脑上体验了一下，梳理了win上实现xiaoaiGPT流程，希望有些帮助。（ps：不建议观看未更新的YouTube教学视频，很多步骤落后与更新的、更方便的代码，甚至会误导）。

首先，下载两个重要的github库：**[xiaogpt](https://github.com/yihong0618/xiaogpt)和[MiService](https://github.com/yihong0618/MiService)**；网络不稳定可以下载压缩包解压到本地，效果是一样的。我将他们分别命名为main和branch区分主次，保持原命名也可以，这只是个人习惯。

```python
文件夹结构如下：
xiaoaiGPT
		main：里面存放xiaoaiGPT库里下载的所有文件
		branch：里面存放MiServive库里下载的文件
```

分别进入branch和main文件夹，在路径栏里输入cmd并按下回车，即可打开命令窗口


## 1。在main文件夹的cmd中

安装依赖

```python
pip install -U xiaogpt
```

## 2.在branch文件夹的cmd中

安装依赖

```python
pip3 install .
```

先设置账号，给没用过小爱音响朋友说一下：**你需要下载app小爱音箱注册一个自己的账号和密码，并且在app中开启蓝牙使得电脑连接上小爱。**

```python
set MI_USER=xxxxx # 不需要引号
set MI_PASS=xxxxxx # 不需要引号
```

查询自己的设备：

```python
python micli.py list
```

运行后出现的字典数据中的did是需要的：

```python
[
  {
    "name": "小爱音箱Pro",
    "model": "xiaomixxxxxxx",
    "did": "xxxxxxxx",
    "token": "506d6xxxxxxx278236789034"
  }
]
```

设置did

```python
set MI_DID=xxxxxxx # 不需要引号
```

## 3.回到main文件夹的cmd中

这里大佬给了配置文件教程，奈何笨蛋的我整明白😂我直接两步启动。 

```python
set OPENAI_API_KEY=xxxxxxx # 无需引号

# hardware 跟你小爱机器型号，可以看看音响的屁股
# --mute_xiaoai让小爱闭嘴
# --use_gpt3有密钥决定，其实大佬还给了chatgpt选项，不过鉴于gpt4都出来了。。。
# --api_base 如果你已跨越高墙则不需要，
# 这是放上一个没有GFW域名，可以让你正常网络下使用xiaoaigpt
# 强调下，大佬说--api_base后面一串需要引号，实测不需要的，加引号报错。。
xiaogpt --hardware 机器型号  --mute_xiaoai --use_gpt3 --api_base https://mydomain/v1
```

如何拥有没被GFW的域名，可以看看**[noobnooc](https://github.com/noobnooc/noobnooc)**的discussion，可谓是非常详尽了。。。
