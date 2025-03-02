# 以下为Substore部署教程
# 基础版
- 前提条件：
一个可以使用的docker，至少120mb的docker空间
或者代理软件内置Substore支持也可以使用
如果你已满足上述条件那么可以进行下一步
## 安装Substore,以openwrt平台为例
打开docker输入以下命令
```
docker run -it -d \
  --name sub-store \
  --restart=always \
  --net=host \
  -e "SUB_STORE_CRON=55 23 * * *" \
  -e "SUB_STORE_FRONTEND_BACKEND_PATH=/CKg2abstVnOeRpm1aB4G" \
  -v /etc/sub-store:/opt/app/data \
  xream/sub-store
```
等待安装完成
### 后台访问
比如路由器网段为192.168.2.0/24
那么如果你要访问Substore后台则须将x改为与路由器同一网段的2将y改为部署substore的openwrt设备的最后一位ip
访问参考代码
```
http://192.168.x.y:3001/subs?api=http://192.168.x.y:3001/CKg2absthskxudnm
```
- 其中这一段CKg2absthskxudnm为Substore访问的安全路径或者说是密码，在公共vps上部署请勿将该段设置得过于简单
- [在线密码生成网站](https://1password.com/zh-cn/password-generator)
## Substore设置部分
打开后台后点击第二页文件管理，创建文件
#### 1.名称部分可自定义但必填
#### 2.选填：显示名称，备注，图标链接，查询流量信息订阅链接，查询流量信息 User-Agent，User-Agent，代理/策略，合并来源
#### 3.关闭，启用下载(文件名为显示名称)
#### 4.类型选择文件，来源选择远程
## 链接部分
标准版填入
```
https://raw.githubusercontent.com/Lanlan13-14/Rules/refs/heads/main/configfull.yaml#noCache
```
NoAd版填入
```
https://raw.githubusercontent.com/Lanlan13-14/Rules/refs/heads/main/configfull_NoAd.yaml#noCache
```
Stash版填入
```
https://raw.githubusercontent.com/Lanlan13-14/Rules/refs/heads/main/configfull_Stash.yaml#noCache
```
## 脚本部分
### 机场链接自动填写
1.创建脚本操作选择脚本，删除原有全部内容
如果要自动填“订阅链接1”则输入
```
$content = $content.replace(/订阅链接1/g, '此处填写订阅链接');
```
以此类推，替换2/3就把（订阅链接1）替换为（订阅链接2）再贴上订阅
### 添加机场备注
```
$content = $content.replace(/机场名称1/g, '此处填写机场备注');
```
替换2/3同理
### 修改webUi面板代理提供者部分显示的名称
```
$content = $content.replace(/Airport_01/g, '此处填写机场备注');
```
### 自动策略组排除指定机场/节点，该功能依赖第二步添加机场备注
我在自动策略组都加入了类似于The_US_automation的无关过滤词供各位替换
比如我想要在美国自动里排除带有“凤凰城”名字的节点那么我只需在脚本处添加如下脚本
```
$content = $content.replace(/The_US_automation/g, '凤凰城');
```
需要在自建/家宽节点自定义过滤的使用以下代码，以过滤HGC为例
```
$content = $content.replace(/The_house/g, 'hgc');
```
这些设置完成后便可以点击保存，复制链接，在同一局域网内如同使用订阅一样使用

### 实在不会的这里提供部署事例
#### nikki订阅要选择本地
![Substore 部署示例1](https://raw.githubusercontent.com/Lanlan13-14/Rules/refs/heads/main/Others/Substore01.jpg)
![Substore 部署示例2](https://raw.githubusercontent.com/Lanlan13-14/Rules/refs/heads/main/Others/Substore02.jpg)
![Substore 部署示例3](https://raw.githubusercontent.com/Lanlan13-14/Rules/refs/heads/main/Others/Substore03.jpg)

# 高级篇
#### 部署同上，请确保Substore版本已为最新版
使用教程如下
- 1 新建文件选择mihomo覆写如图
![Substore高级01](https://raw.githubusercontent.com/Lanlan13-14/Rules/refs/heads/main/Others/Substore%E9%AB%98%E7%BA%A701.jpg)
- 2 新建后名称自定义一个不重复的
- 3 类型-选择mihomo配置
- 4 来源-选择无
- 5 若想自定义配置名称那么在显示名称那里输入并开启启用下载，如图
![Substore高级02](https://raw.githubusercontent.com/Lanlan13-14/Rules/refs/heads/main/Others/Substore%E9%AB%98%E7%BA%A702.png)
- 6 其余选项个人需要填写
## 链接部分（🔗链接一定要放在第一个脚本处）
- 1 新建一个脚本
标准版填入
```
https://raw.githubusercontent.com/Lanlan13-14/Rules/refs/heads/main/configfull.yaml#noCache
```
NoAd版填入
```
https://raw.githubusercontent.com/Lanlan13-14/Rules/refs/heads/main/configfull_NoAd.yaml#noCache
```
Stash版填入
```
https://raw.githubusercontent.com/Lanlan13-14/Rules/refs/heads/main/configfull_Stash.yaml#noCache
```
- 2 新建一个脚本以替换订阅及名称所需代码与基础篇一致包括自定义过滤部分

