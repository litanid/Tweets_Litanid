
# 说明

本 repository 为 litanid 的完整历史 tweets 存档备份，浏览地址为 https://litanid.github.io/Tweets_Litanid ，不定时更新。实时更新（每天00:00更新）存档见本人博客 https://www.yiwan.pro/tweetslitanid/ 。推文初始归档从推特官网打包下载，后续更新采用 grailbird_update ( https://github.com/DeMarko/grailbird_updater )每日更新。

此文参考借鉴 https://github.com/wastemobile/mytweets 。 


# Twitter 存档

每个人都能从 Twitter “个人资料与账号”-“设置与隐私” 管理页申请自己的 Twitter 推文存档，申请后需要一点时间（差不多是马上），你会得到一个压缩包。解压里不但有两种格式的所有历史推文，还包含一个极简单、却又很完整的静态网站。

使用你的 Twitter 推文存档最简单的方法就是通过存档提供的浏览界面，只要双击根目录的 `index.html` 就能够在浏览器里浏览你的全部推文历史。

你甚至可以将整个目录摆到真正的网站上，就像是一个正常、一般的静态网站，让你很容易点击进入某年某月的推文整理，甚至还有搜寻功能。因为搜寻对象真的就是你所有的推文，因此任何时间的推都可以搜寻得到，比 Twitter 网站还好用（怎么会这样？）。

# 持续更新

当然这个存档，只到你申请下载的那个时间点而已，于是有大神写了小程序，可以让我们能够持续更新。

https://github.com/DeMarko/grailbird_updater

此更新程序采用 `ruby` 编写，详细安装说明见大神 repository 。
此处只列明 Debian 环境下如何安装使用，其他环境自行修改，步骤如下：

1.安装ruby
```
aptitude install ruby
sudo gem install grailbird_updater
```

2.解压从推特官网下载的推文归档包，假设解压到 Tweets-Litanid 文件夹，文件夹路径为 `/home/litanid/litanid_Temporary/Tweets_Litanid/`。

3.在`https://apps.twitter.com/`上新建app，命名假设为 Grailbird-Litanid 。 Generate Consumer Key and Secret ，Generate Access Token and Token Secret ，复制记录产生的 Key、Token 和 Secret并设置读写权限，其它内容自行填写。

4.在终端运行命令：
```
grailbird_updater  /home/litanid/litanid_Temporary/Tweets_Litanid/
```
需要输入个人 twitter 账号（此例为 litanid ）相关信息和上面产生的Key、Token 和 Secret 。
这些信息会存储到文件`/home/litanid/litanid_WWW/Tweets_Litanid//litanid_keys.yaml`当中。为安全起见，此文件最好移出放到其他目录。
此命令成功运行一次即可，不用执行第二次。

5.设置每天自动更新：
用 root 用户登录终端，执行`crontab -e`，添加：
```
@daily /bin/bash -l -c 'grailbird_updater /home/litanid/litanid_WWW/Tweets_Litanid'
```
如 litanid_keys.yaml 移出来到`/home/litanid`目录，则上面命令要修改为
```
@daily /bin/bash -l -c 'grailbird_updater --key-path=/home/litanid /home/litanid/litanid_WWW/Tweets_Litanid'
```

# 网站浏览

如上设置后，只要推特有推文发布，grailbird_updater 每天00:00便会推特官网数据库提取相关信息，更新 Tweets_Litanid 目录下的文件，主要是更新添加 /data/js/tweets/ 下的 js 文件。只要双击 Tweets_Litanid 根目录的 `index.html` 就能够在浏览器里浏览的全部推文历史。

当然，也可以自己设置 Web 服务器，单独浏览推文历史。本人就在自己博客上设置单独设置了二级目录浏览，网址是： https://www.yiwan.pro/tweetslitanid/ 。

另外，也可以利用 GitHub 提供的静态网站服务建立 GitHub Pages 浏览。单独建立一个 repository ，如本 repository 名为 Tweets_Litanid 。通过 git 实时 push 本地建立的 Tweets_Litanid 目录内容至 github 上的 Tweets_Litanid 仓库，再设置好 Pages ，即可浏览。本 Tweets_Litanid 仓库浏览地址为 https://litanid.github.io/Tweets_Litanid 。本 repository 尚未与 https://www.yiwan.pro/tweetslitanid/ 上的内容保持同步，留待以后不定期更新。

# 尚存问题

细心的网友浏览推文历史备份时会发现，以从 Twitter 官网下载推文存档包为时间分界点，之前的推文不会显示 Tweet 的时间，而之后的就显示。此问题留待以后研究解决。 