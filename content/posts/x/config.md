+++
date = '2024-12-22T01:25:59-04:00'
draft = false
title = 'Config'
+++

```
; 2021-01-16：增加对各个模块的说明(某些内容只适用于 1.0.14 以上版本)
;⚠️注意⚠️: 以下内容中，带“;” “#”的都是注释符号，去掉前面的符号，该行才有效

;general 模块内为一些通用的设置参数项
[general]
;Quantumult X 会对 server_check_url 指定的网址进行相应测试，以确认节点的可用性
;你同样可以在 server_local/remote 中，为节点、订阅单独指定server_check_url参数
server_check_url= http://www.google.com/generate_204
server_check_timeout=3000
;👍👍👍资源解析器，可用于自定义各类远程资源的转换，如节点，规则 filter，复写 rewrite 等，url 地址可远程，可 本地/iCloud(Quantumult X/Scripts目录);
;下面是我写的一个解析器，具体内容直接参照链接里的使用说明
resource_parser_url= https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/resource-parser.js

;👍👍geo_location_checker用于节点页面的节点信息展示，可完整自定义展示内容与方式
; extreme-ip-lookup为Quantumult X 作者提供的示范 api
;geo_location_checker=http://extreme-ip-lookup.com/json/, https://raw.githubusercontent.com/crossutility/Quantumult-X/master/sample-location-with-script.js
;下面是我所使用的 api 及获取、展示节点信息的 js
geo_location_checker=http://ip-api.com/json/?lang=zh-CN, https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/IP_API.js

excluded_routes=239.255.255.250/32, 24.105.30.129/32, 185.60.112.157/32, 185.60.112.158/32, 182.162.132.1/32
udp_whitelist=1-442, 444-65535

;👍👍👍运行模式模块，running_mode_trigger 设置，即根据网络自动切换 分流/直连/全局代理 等模式。
;running-mode-trigger 模式下，跟手动切换直连/全局代理 等效，rewrite/task 模块始终会生效，比 ssid 策略组设置简单，比 ssid-suspend 更灵活。

;running_mode_trigger=filter, filter, asus-5g:all_direct, asus: all_proxy
; 上述写法，前两个 filter 表示 在 4G 网络跟一般 Wi-Fi 下，走 filter(分流)模式，asus-5g 则切换为全局直连，asus 切换为全局代理
; 如需使用，相应 SSID 换成你自己 Wi-Fi 名即可


;ssid_suspended_list，让 Quantumult X 在特定 Wi-Fi 网络下暂停工作(仅 task 模块会继续工作)，多个Wi-Fi用“,”连接
;ssid_suspended_list=Asus, Shawn-Wifi

;dns exclusion list中的域名将不使用fake-ip方式. 其它域名则全部采用 fake-ip 及远程解析的模式
;dns_exclusion_list=*.qq.com, qq.com
dns_exclusion_list=*.cmpassport.com, *.jegotrip.com.cn, *.icitymobile.mobi, id6.me, *.pingan.com.cn

;UDP名单，留空则默认所有为端口。不在udp白名单列表中的端口，将被丢弃处理。
;udp_whitelist=53, 123, 1900, 80-443

;下列表中的内容将不经过 QuantumultX的处理
;excluded_routes= 192.168.0.0/16, 172.16.0.0/12, 100.64.0.0/10, 10.0.0.0/8
;icmp_auto_reply=true

[dns]
;指定的 dns服务器
server=8.8.8.8
server=114.114.114.114
server=202.141.176.93 
server=202.141.178.13
server=117.50.10.10
server=223.5.5.5
server=119.29.29.29:53
server=119.28.28.28
;指定域名解析dns
server=/*.taobao.com/223.5.5.5
server=/*.tmall.com/223.5.5.5
server=/*.alipay.com/223.5.5.5
server=/*.alicdn.com/223.5.5.5
server=/*.aliyun.com/223.5.5.5
server=/*.jd.com/119.28.28.28
server=/*.qq.com/119.28.28.28
server=/*.tencent.com/119.28.28.28
server=/*.weixin.com/119.28.28.28
server=/*.bilibili.com/119.29.29.29
server=/hdslb.com/119.29.29.29
server=/*.163.com/119.29.29.29
server=/*.126.com/119.29.29.29
server=/*.126.net/119.29.29.29
server=/*.127.net/119.29.29.29
server=/*.netease.com/119.29.29.29
server=/*.mi.com/119.29.29.29
server=/*.xiaomi.com/119.29.29.29
;server=/*testflight.apple.com/23.76.66.98
;server=8.8.8.8
;server=/example1.com/8.8.4.4
;server=/*.example2.com/223.5.5.5
;server=/example4.com/[2001:4860:4860::8888]:53
;address=/example5.com/192.168.16.18
;address=/example6.com/[2001:8d3:8d3:8d3:8d3:8d3:8d3:8d3]



[task_local]
;任务模块，可用于签到,天气话费查询等
;js文件放于iCloud或者本机的Quantumult X/Scripts 路径下。TF版本可直接使用远程js链接

;2 12 * * * sample.js, tag=本地示范(左滑编辑，右滑执行), img-url=https://raw.githubusercontent.com/crossutility/Quantumult-X/master/quantumult-x.png
;13 12 * * * https://raw.githubusercontent.com/crossutility/Quantumult-X/master/sample-task.js, tag=远程示范(点击缓存/更新脚本), img-url=https://raw.githubusercontent.com/crossutility/Quantumult-X/master/quantumult-x.png
;从 “分” 开始的5位cron 写法，具体 cron 表达式可自行 Google
;比如上述语句 代表每天 12 点 2 分，自动执行一次;
;tag参数为 task 命名标识;
;img-url参数用于指定 task 的图标(108*108)
# > 请手动添加下面的订阅（流媒体Task订阅集合）
; https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/UI-Action.json
# > 流媒体解锁查询
event-interaction https://raw.githubusercontent.com/KOP-XIAO/QuantumultX/master/Scripts/streaming-ui-check.js, tag=流媒体解锁查询, img-url=arrowtriangle.right.square.system, enabled=true

#以下为策略组[policy]部分
# static 策略组中，你需要手动选择想要的节点/策略组。
# available 策略组将按顺序选择你列表中第一个可用的节点。
# round-robin 策略组，将按列表的顺序轮流使用其中的节点。
# ssid 策略组，将根据你所设定的网络来自动切换节点/策略组
;img-url 参数用于指定策略组图标，可远程，也可本地/iCloud(Quantumult X/Images路径下) （108*108 大小）
;direct/proxy/reject 则只能用本地图标，名字分别为 direct.png, proxy.png,reject.png 放置于 Images 文件夹下即可生效 (108*108 大小)

[policy]
;url-latency-benchmark=auto, server-tag-regex=(?=.*), check-interval=10, tolerance=50, img-url=https://raw.githubusercontent.com/Orz-3/mini/master/Color/Urltest.png
;static=🍎 苹果服务, direct, proxy, img-url= https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Apple.png
;static=💻 国外影视, proxy, direct, img-url= https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/ForeignMedia.png
;static=📽 国内视频, direct, proxy, img-url= https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/DomesticMedia.png
;static=🎬 YouTube, proxy, direct, img-url= https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/YouTube.png
;static=📺 Netflix, proxy, direct, img-url= https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Netflix_Letter.png
;static=🌏 国外网站, proxy,direct,🇭🇰️ 香港(正则示范), img-url= https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Global.png
static=OpenAI, direct, img-url=https://raw.githubusercontent.com/Orz-3/mini/master/Color/Streaming.png
;static= 🇭🇰️ 香港(正则示范), server-tag-regex= 香港|🇭🇰️|HK|Hong, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/HK.png
static=🕹 终极清单, direct, proxy, img-url=https://raw.githubusercontent.com/Orz-3/mini/master/Color/Final.png
static=网易云音乐, direct, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Netease_Music_Unlock.png
static=全球加速, proxy, direct, img-url=https://raw.githubusercontent.com/Orz-3/mini/master/Color/Global.png
static=苹果服务, direct, proxy, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Apple.png
static=哔哩哔哩, direct, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/bilibili.png
static=国际媒体, proxy, img-url=https://raw.githubusercontent.com/Orz-3/mini/master/Color/Streaming.png


#server-tag-regex 以及 resource-tag-regex 参数用于正则筛选来建立策略组
#具体可参见教程部分: https://shrtm.nu/DAFP

#以下是quantumultX的3普通种策略组类型写法
;static=policy-name-1, Sample-A, Sample-B, Sample-C
;available=policy-name-2, Sample-A, Sample-B, Sample-C
;round-robin=policy-name-3, Sample-A, Sample-B, Sample-C
#下面是ssid策略组示范
;ssid=policy-name-4, Sample-A, Sample-B, LINK_22E171:Sample-B, LINK_22E172:Sample-C


# "tag" 跟 "enabled" 为可选参数，分别表示 “标签”及“开启状态”, true 为开启，false 关闭.
# update-interval 为更新时间参数，单位 秒, 默认更新时间为 24*60*60=86400 秒，也就是24小时.
# opt-parser=true/false 用于控制是否对本订阅 开启资源解析器，不写或者 false 表示不启用解析器;

#服务器远程订阅
[server_remote]
#远程服务器订阅模块，可直接订阅SSR，SS链接，以及Quantumult X格式的vmess/trojan/https订阅
#其它格式可用 opt-parser 参数开启解析器导入使用
#img-url参数用于指定图标，格式要求同样为 108*108 的 png 图片，可远程，可本地
;https://raw.githubusercontent.com/crossutility/Quantumult-X/master/server.txt#rename=[香港], tag=示范(请先导入自己订阅/节点), update-interval=86400, opt-parser=true,  img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Quantumult_X.png, enabled=true
;https://raw.githubusercontent.com/crossutility/Quantumult-X/master/server-complete.txt, tag=示范(导入后更新并删除示范),  img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Quantumult_X.png, enabled=true

#支持本地/iCloud的节点文件，位于Quantumult X/Profiles路径下
;servers.txt, tag=本地服务器, img-url=https://raw.githubusercontent.com/crossutility/Quantumult-X/master/quantumult-x.png, enabled=false

#规则分流远程订阅
[filter_remote]
#远程分流模块，可使用force-policy来强制使用策略偏好, 替换远程规则内所指定的策略组
;同样的
# update-interval 为更新时间参数，单位 秒, 默认更新时间为 24*60*60=86400 秒，也就是24小时.
# opt-parser=true/false 用于控制是否对本订阅 开启资源解析器，不写或者 false 表示不启用解析器;


;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Filter/Guard/Advertising.list, tag=🚦去广告, update-interval=86400, opt-parser=true, enabled=true

;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Filter/Guard/Hijacking.list, tag=🚫 运营商劫持, enabled=true

;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Filter/StreamingMedia/StreamingCN.list, force-policy=📽 国内视频, tag=📽 国内视频, enabled=true

;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Filter/StreamingMedia/Video/Netflix.list, tag=📺 Netflix, force-policy=📺 Netflix, enabled=true

;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Filter/StreamingMedia/Video/YouTube.list, tag=🎬 YouTube, force-policy=🎬 YouTube, enabled=true

;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Filter/StreamingMedia/Streaming.list, tag=💻 国外影视,force-policy= 💻 国外影视, enabled=true

;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Filter/Global.list, tag=🌍 国外网站, force-policy= 🌏 国外网站, enabled=true

;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Filter/Extra/Apple/Apple.list, tag= Apple服务, force-policy=🍎 苹果服务,enabled=true

;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Filter/Extra/Apple/BlockiOSUpdate.list, tag= 屏蔽更新,enabled=true

;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Filter/China.list, tag=🐼 国内网站, enabled=true

;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Filter/Extra/ChinaIP.list, tag=🇨🇳️ 国内IP池, enabled=true
https://github.com/ddgksf2013/Filter/raw/master/NeteaseMusic.list, tag=解锁网易云音乐, force-policy=网易云音乐, update-interval=172800, opt-parser=false, enabled=true
https://raw.githubusercontent.com/ddgksf2013/Filter/master/Unbreak.list, tag=规则修正, force-policy=direct, update-interval=172800, opt-parser=true, enabled=true
https://raw.githubusercontent.com/Cats-Team/AdRules/main/qx.conf, tag=广告终结者, force-policy=reject, update-interval=172800, opt-parser=true, enabled=true
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/WeChat/WeChat.list, tag=微信直连, force-policy=direct, update-interval=172800, opt-parser=false, enabled=true
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/TikTok/TikTok.list, tag=海外抖音, force-policy=全球加速, update-interval=172800, opt-parser=true, enabled=true
https://raw.githubusercontent.com/ddgksf2013/Filter/master/GoogleVoice.list, tag=Google Voice, force-policy=proxy, update-interval=172800, opt-parser=true, enabled=true
https://github.com/blackmatrix7/ios_rule_script/raw/master/rule/QuantumultX/OpenAI/OpenAI.list, tag=OpenAi, force-policy=direct, update-interval=172800, opt-parser=true, enabled=true
;https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/Spotify/Spotify.list, tag=Spotify音乐, force-policy=香港节点, update-interval=172800, opt-parser=true, enabled=true
https://raw.githubusercontent.com/ddgksf2013/Filter/master/Streaming.list, tag=国际媒体, force-policy=国际媒体, update-interval=172800, opt-parser=true, enabled=true
https://raw.githubusercontent.com/ddgksf2013/Filter/master/StreamingSE.list, tag=哔哩哔哩, force-policy=哔哩哔哩, update-interval=172800, opt-parser=true, enabled=true
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/Apple/Apple.list, tag=苹果服务, force-policy=苹果服务, update-interval=172800, opt-parser=true, enabled=true
https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/ProxyGFWlist.list, tag=全球加速, force-policy=全球加速, update-interval=172800, opt-parser=true, enabled=true
https://raw.githubusercontent.com/VirgilClyne/GetSomeFries/main/ruleset/ASN.China.list, tag=国内网站, force-policy=direct, update-interval=172800, opt-parser=true, enabled=true
;https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/QuantumultX/OpenAI/OpenAI.list, tag=OpenAI, force-policy=OpenAI, update-interval=172800, opt-parser=true, enabled=true


#支持本地/iCloud规则文件，位于Quantumult X/Profiles路径下
;filter.txt, tag=本地分流, enabled=false

#rewrite 复写远程订阅
[rewrite_remote]
#远程复写模块，内包含主机名hostname以及复写rewrite规则
# update-interval 为更新时间参数，单位 秒, 默认更新时间为 24*60*60=86400 秒，也就是24小时.
# opt-parser=true/false 用于控制是否对本订阅 开启资源解析器，不写或者 false 表示不启用解析器;


# https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Rewrite/Block/Advertising.conf, tag=神机复写(⛔️去广告), update-interval=86400, opt-parser=false, enabled=true

;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Rewrite/General.conf, tag=神机复写(😄️通用), update-interval=86400, opt-parser=false, enabled=true

;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Rewrite/Unlock/TikTokJP.conf, tag=神机复写(🎵️TikTok-JP), update-interval=86400, opt-parser=false, enabled=false

;Youtube premium 会员请勿开启此条
;https://raw.githubusercontent.com/DivineEngine/Profiles/master/Quantumult/Rewrite/Block/YouTubeAds.conf, tag=神机复写(🈲YouTube-AD), update-interval=86400, opt-parser=false, enabled=true

;https://raw.githubusercontent.com/Orz-3/QuantumultX/master/YouTube.conf, tag=Orz(🈲YouTube-AD), update-interval=86400, opt-parser=false, enabled=true

# ======= 会员解锁 ======= #
https://github.com/ddgksf2013/Rewrite/raw/master/AdBlock/Bilibili.conf, tag=哔哩哔哩广告净化@ddgksf2013, update-interval=86400, opt-parser=false, enabled=true
https://github.com/ddgksf2013/Rewrite/raw/master/UnlockVip/Spotify.conf, tag=Spotify音乐VIP[音质≤高]@app2smile, update-interval=86400, opt-parser=false, enabled=true
https://github.com/ddgksf2013/dev/raw/master/ForOwnUse.conf, tag=墨鱼专属VIP@ddgksf2013, update-interval=86400, opt-parser=false, enabled=true


# ======= 广告净化 ======= #
https://github.com/ddgksf2013/Rewrite/raw/master/AdBlock/StartUp.conf, tag=墨鱼去开屏2.0@ddgksf2013, update-interval=86400, opt-parser=false, enabled=true
https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/script/zheye/zheye.snippet, tag=知乎去广告及体验增强@blackmatrix7, update-interval=86400, opt-parser=false, enabled=true
https://github.com/app2smile/rules/raw/master/module/tieba-qx.conf, tag=百度贴吧去广告@app2smile, update-interval=86400, opt-parser=false, enabled=false
https://github.com/ddgksf2013/Rewrite/raw/master/AdBlock/Applet.conf, tag=微信小程序去广告@ddgksf2013, update-interval=86400, opt-parser=false, enabled=true
https://github.com/ddgksf2013/Rewrite/raw/master/AdBlock/YoutubeAds.conf, tag=油管去广告@Maasea, update-interval=86400, opt-parser=false, enabled=true
https://github.com/ddgksf2013/Rewrite/raw/master/AdBlock/Weibo.conf, tag=微博去广告@ddgksf2013, update-interval=86400, opt-parser=false, enabled=true
https://github.com/ddgksf2013/Rewrite/raw/master/AdBlock/Ximalaya.conf, tag=喜马拉雅去广告[卸载重装]@ddgksf2013, update-interval=86400, opt-parser=false, enabled=true
https://github.com/ddgksf2013/Rewrite/raw/master/AdBlock/Amap.conf, tag=高德地图净化[卸载重装]@ddgksf2013, update-interval=86400, opt-parser=false, enabled=true
https://github.com/ddgksf2013/Rewrite/raw/master/AdBlock/Netease.conf, tag=网易云音乐去广告[卸载重装]@ddgksf2013, update-interval=86400, opt-parser=false, enabled=false
https://gist.githubusercontent.com/ddgksf2013/beec132ca0c3570ffa0cf331bce8f82a/raw/baidumap.adblock.conf, tag=百度地图净化[卸载重装]@ddgksf2013, update-interval=86400, opt-parser=false, enabled=false


# ======= 网页优化 ======= #
https://github.com/ddgksf2013/Rewrite/raw/master/Html/WebAdBlock.conf, tag=影视网站去广告@ddgksf2013, update-interval=86400, opt-parser=false, enabled=true
https://github.com/ddgksf2013/Rewrite/raw/master/Html/Q-Search.conf, tag=Safari超级搜索@ddgksf2013, update-interval=86400, opt-parser=false, enabled=true
https://github.com/ddgksf2013/Rewrite/raw/master/Html/Douban.conf, tag=豆瓣网页观影快捷跳转@ddgksf2013, update-interval=86400, opt-parser=false, enabled=true
https://raw.githubusercontent.com/ddgksf2013/Rewrite/master/Html/General.conf, tag=神机重定向@DivineEngine, update-interval=86400, opt-parser=false, enabled=true


# ======= 功能增强 ======= #
https://github.com/ddgksf2013/Rewrite/raw/master/AdBlock/XiaoHongShu.conf, tag=小红书净化+去水印@ddgksf2013, update-interval=86400, opt-parser=false, enabled=true
https://gist.githubusercontent.com/ddgksf2013/f43026707830c7818ee3ba624e383c8d/raw/baiduCloud.vip.js, tag=百度网盘净化+倍速@ddgksf2013, update-interval=86400, opt-parser=true, enabled=false
https://raw.githubusercontent.com/ddgksf2013/Rewrite/master/Function/UnblockURLinWeChat.conf, tag=微信解锁被屏蔽的URL@zZPiglet, update-interval=86400, opt-parser=false, enabled=true


# ======= 自行启用 ======= #
https://raw.githubusercontent.com/Orz-3/QuantumultX/master/Netflix_ratings.conf, tag=Netflix评分@Orz-3, update-interval=86400, opt-parser=false, enabled=false
https://raw.githubusercontent.com/id77/QuantumultX/master/rewrite/Youtube_CC.conf#out=Hant, tag=油管字幕翻译@id77, update-interval=86400, opt-parser=false, enabled=false
;https://raw.githubusercontent.com/chavyleung/scripts/master/box/rewrite/boxjs.rewrite.quanx.conf, tag=BoxJS商店版@chavyleung, update-interval=86400, opt-parser=false, enabled=false

#支持本地/iCloud的复写规则文件，位于Quantumult X/Profiles路径下
;rewrite.txt, tag=本地复写, opt-parser=false, enabled=false

# 本地服务器部分
[server_local]
# 以下示范都是 ip(域名):端口，
# 比如 vmess-a.203.167.55.4:777 ，实际是 203.167.55.4:777
# 前面的 ss-a，ws-tls这些，只是为了让你快速找到自己节点的类型
# 实际使用时，请不要真的 傻乎乎的 写 vmess-a.203.167.55.4:777 这种。

#shadowsocks以及shadowsocksR类型
;shadowsocks=ss-a.example.com:80, method=chacha20, password=pwd, obfs=http, obfs-host=bing.com, obfs-uri=/resource/file, fast-open=false, udp-relay=false, server_check_url=http://www.apple.com/generate_204, tag=Sample-A
;shadowsocks=ss-b.example.com:80, method=chacha20, password=pwd, obfs=http, obfs-host=bing.com, obfs-uri=/resource/file, fast-open=false, udp-relay=false, tag=Sample-B
;shadowsocks=ss-c.example.com:443, method=chacha20, password=pwd, obfs=tls, obfs-host=bing.com, fast-open=false, udp-relay=false, tag=Sample-C
;shadowsocks=ssr-a.example.com:443, method=chacha20, password=pwd, ssr-protocol=auth_chain_b, ssr-protocol-param=def, obfs=tls1.2_ticket_fastauth, obfs-host=bing.com, tag=Sample-D
;shadowsocks=ws-a.example.com:80, method=aes-128-gcm, password=pwd, obfs=ws, obfs-uri=/ws, fast-open=false, udp-relay=false, tag=Sample-E
;shadowsocks=ws-b.example.com:80, method=aes-128-gcm, password=pwd, obfs=ws, fast-open=false, udp-relay=false, tag=Sample-F
;shadowsocks=ws-tls-a.example.com:443, method=aes-128-gcm, password=pwd, obfs=wss, obfs-uri=/ws, fast-open=false, udp-relay=false, tag=Sample-G

# vmess 类型，ws，wss(ws+tls),over-tls,tcp 
; ws 类型
;vmess=ws-c.example.com:80, method=chacha20-ietf-poly1305, password= 23ad6b10-8d1a-40f7-8ad0-e3e35cd32291, obfs-host=ws-c.example.com, obfs=ws, obfs-uri=/ws, fast-open=false, udp-relay=false, tag=Sample-H
; wss(ws+tls) 类型
;vmess=ws-tls-b.example.com:443, method=chacha20-ietf-poly1305, password= 23ad6b10-8d1a-40f7-8ad0-e3e35cd32291, obfs-host=ws-tls-b.example.com, obfs=wss, obfs-uri=/ws, tls-verification=true,fast-open=false, udp-relay=false, tag=Sample-I
;vmess=cdn1.welovesharin9.ga:443, method=chacha20-ietf-poly1305, password=eaf163fe-978b-4bbf-9950-bf87b8d2a5ca, obfs-host=cdn1.welovesharin9.ga, obfs=wss, obfs-uri=/ichi, tls-verification=true,fast-open=false, udp-relay=false, tag=cdn1.ga
; tcp 类型
;vmess=vmess-a.example.com:80, method=aes-128-gcm, password=23ad6b10-8d1a-40f7-8ad0-e3e35cd32291, fast-open=false, udp-relay=false, tag=Sample-J
;vmess=vmess-b.example.com:80, method=none, password=23ad6b10-8d1a-40f7-8ad0-e3e35cd32291, fast-open=false, udp-relay=false, tag=Sample-K
; over-tls 类型
;vmess=vmess-over-tls.example.com:443, method=none, password=23ad6b10-8d1a-40f7-8ad0-e3e35cd32291, obfs-host=vmess-over-tls.example.com, obfs=over-tls, tls-verification=true, fast-open=false, udp-relay=false, tag=Sample-L

; http(s) 类型
;http=http.example.com:80, username=name, password=pwd, fast-open=false, udp-relay=false, tag=http
;http=https.example.com:443, username=name, password=pwd, over-tls=true, tls-verification=true, tls-host=example.com, tls-verification=true, fast-open=false, udp-relay=false, tag=http-tls

; trojan 类型
;trojan=example.com:443, password=pwd, over-tls=true, tls-verification=true, fast-open=false, udp-relay=false, tag=trojan-tls-01
trojan=cdn1.welovesharin9.gq:443, password=trump2o2o, over-tls=true, tls-host=cdn1.welovesharin9.gq, tls-verification=true, tls13=true, fast-open=false, udp-relay=false, tag=cdn1
trojan=kora0.flz.ca:443,password=trump2o2o, over-tls=true, tls-host=kora0.flz.ca, tls-verification=true, tls13=true, fast-open=false, udp-relay=false, tag=kora0
trojan=kora1.flz.ca:443, password=trump2o2o, over-tls=true, tls-host=kora1.flz.ca, tls-verification=true, tls13=true, fast-open=false, udp-relay=false, tag=kora1
trojan=kora2.flz.ca:443, password=trump2o2o, over-tls=true, tls-host=kora2.flz.ca, tls-verification=true, tls13=true, fast-open=false, udp-relay=false, tag=kora2
trojan=kora3.flz.ca:443, password=trump2o2o, over-tls=true, tls-host=kora3.flz.ca, tls-verification=true, tls13=true, fast-open=false, udp-relay=false, tag=kora3
trojan=tor1.flz.ca:443, password=trump2o2o, over-tls=true, tls-host=tor1.flz.ca, tls-verification=true, tls13=true, fast-open=false, udp-relay=false, tag=tor1
trojan=osk0.flz.ca:443,password=trump2o2o, over-tls=true, tls-host=osk0.flz.ca, tls-verification=true, tls13=true, fast-open=false, udp-relay=false, tag=osk0
trojan=cdn1.welovesharin9.workers.dev:443, password=trump2o2o, over-tls=true, tls-host=cdn1.welovesharin9.workers.dev, tls-verification=true, tls13=true, fast-open=false, udp-relay=false, tag=cf1
#本地分流规则(对于完全相同的某条规则，本地的将优先生效)
[filter_local]
# > 一些比较容易忽视的分流
host, ad.12306.cn, direct
host, gg.caixin.com, direct
host, sdkapp.uve.weibo.com, direct
host-suffix, ucweb.com, direct
host-suffix, kuwo.cn, direct
host, ntb.lanjie100.com, reject

# > 贴吧屏蔽域名dns查询
ip-cidr, 180.76.76.200/32, reject

host-wildcard, *.googlevideo.com, direct
host-suffix, yahoo.com, 全球加速
host, dns.weixin.qq.com, direct
host-suffix, activision.com, proxy
host-keyword, codm, proxy
host-suffix, unionpay.com, direct
host-suffix, 95516.com, direct
host-suffix, amap.com, direct
host-suffix, office.com, direct
host-suffix, office365.com, direct
host-suffix, live.com, direct
host-suffix, outlook.com, direct
;user-agent, ?abc*, proxy
;host, www.google.com, proxy
;host-keyword, adsite, reject
;host-suffix, googleapis.com, proxy
ip-cidr, 10.0.0.0/8, direct
ip-cidr, 127.0.0.0/8, direct
ip-cidr, 172.16.0.0/12, direct
ip-cidr, 192.168.0.0/16, direct
ip-cidr, 224.0.0.0/24, direct
# 已采用 ip 池数据，因此注释掉 geoip cn
;geoip, cn, direct

#不在上述规则中(远程以及本地)的剩余请求，将走final 指定的节点/策略，这里即是 → 🕹 终极清单, 请根据自己的需求来选择直连或节点、策略
final, 🕹 终极清单


#本地复写规则
[rewrite_local]
#去微信公众号广告
;^https?://(sdk|wb)app\.uve\.weibo\.com(/interface/sdk/sdkad.php|/wbapplua/wbpullad.lua) url script-response-body https://raw.githubusercontent.com/yichahucha/surge/master/wb_launch.js
;^https?://m?api\.weibo\.c(n|om)/2/(statuses/(unread|extend|positives/get|(friends|video)(/|_)(mix)?timeline)|stories/(video_stream|home_list)|(groups|fangle)/timeline|profile/statuses|comments/build_comments|photo/recommend_list|service/picfeed|searchall|cardlist|page|!/(photos/pic_recommend_status|live/media_homelist)|video/tiny_stream_video_list|photo/info) url script-response-body https://raw.githubusercontent.com/yichahucha/surge/master/wb_ad.js


#以下为证书&主机名部分
[mitm]
passphrase = CB8370B7
p12 = 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
;以下模块去掉;才生效
;请自行在 APP 的UI中生成证书 并安装&信任
;skip_validating_cert = false
;force_sni_domain_name = false
;hostname = api.weibo.cn, mapi.weibo.com, *.uve.weibo.com
;passphrase = 
;p12 = 
```