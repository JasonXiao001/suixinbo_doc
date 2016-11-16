# SPEAR引擎流控配置简介
###**在进行实际开发前，首先要在腾讯云互动直播配置流控参数，才能获得更好的视频效果。**

# 一、入口
登录腾讯云后，从 “云产品” -> “互动直播” 进入配置页面。
![](https://mc.qcloudimg.com/static/img/243044a017149d82e7cc10a1a81a7c80/image001.png)

进入“互动直播”配置页面后，可以看到自己创建的不同appid对应的配置。鼠标放在“更多”上，选择“SPEAR引擎配置”。

![](https://mc.qcloudimg.com/static/img/864d6de4bf6a052e3c3fb420be59713b/image002.png)

进入后就可以看到具体的参数配置。后面会详细说明配置的含义和如何设置参数。

![](https://mc.qcloudimg.com/static/img/24d35157346b545e20eab9718f2e4856/image004.png)

# 二、配置说明
## 1. 场景
互动直播的配置首先分为不同的场景，每个场景保存自己的配置参数。一个appid可以设置一种对应的场景，当切换场景时，所有的音视频参数都会切换。
目前互动直播主要支持两种场景的业务：互动直播和实时通信。

![](https://mc.qcloudimg.com/static/img/f183e7a8c76ca9895318ae912c917523/image006.png)
![](https://mc.qcloudimg.com/static/img/7587343a15d6a8c31d7fcf13ddb52cff/image007.png)

互动直播主要针对一个或少量几个主播在直播，其他大多数的观众观看的场景。只有一个或几个用户有上行数据，其他大多数用户（几百、几千或更多）只有下行数据，没有上行数据。
实时通信主要针对多人聊天或多人会议的场景。参与的用户都有上下行数据的需要，同时需要较高的实时性，延时要小。
针对不同的场景，提供更适合业务需要的参数配置。

## 2. 平台
每个场景中包含不同平台的配置，支持根据不同的平台设置平台相关的不同参数。目前支持Windows、Web、iOS、Android四个平台，其中Windows和Web的参数配置是统一的。这样设置好后，Windows客户端会自动使用Windows页面的配置，iOS客户端会自动使用iOS页面的配置，以此类推。

![](https://mc.qcloudimg.com/static/img/c90c047e8f64b4085aa5a90eaa0a18a7/image008.png)

## 3. 角色
具体的某一平台的配置中，可以添加多个角色。角色实现了在单一平台上也可以配置不同的参数，即同一客户端可以通过切换角色来实现改变音视频配置的策略。
user是默认角色，当客户端没有选择角色时，会使用默认角色的配置。

![](https://mc.qcloudimg.com/static/img/7da63a7a27f54b153c31d838263e3c2c/image010.png)

可以在页面的最底部添加角色，角色名称设置角色名。角色可以编辑，自己添加的角色可以删除。角色可以根据业务需要添加多个。

![](https://mc.qcloudimg.com/static/img/47ebdf9ebf1a765c0e3105c84fb59da8/image012.png)
![](https://mc.qcloudimg.com/static/img/69996113f9f8dcd94de3a6e6bf17c5d2/image014.png)


## 4. 场景、平台、角色的不同
场景、平台、角色都可以用来设置不同的配置方案，他们之间有什么区别？
场景是应用层面的不同，即一个app是主要用于直播还是实时通话。直播对清晰度流畅度要求高、延时要求低，实时通话对延时要求高；所以互动直播和实时通信的很多配置项都是不同的。一般一个app选择一个场景后，后续不会再改变。平台很容易理解，主要处理平台相关的不同配置，比如PC的性能一般比手机高，手机上的app会有权限的要求的等等。

角色上的区分，主要是为了业务层面的支持。不同角色可设置的配置项和取值范围都是一样的，配置的不同完全由业务决定。比如，作为主播时使用可以上行数据的配置，作为观众时使用只有下行数据的配置；性能高的机器上使用分辨率更高的配置等等。


## 5. 参数配置
参数配置分为视频参数、音频参数、网络参数三部分。在互动直播场景下，视频参数和大部分音频参数（下图红框中的参数）主要应用于上行数据，即只对主播起作用，对观众不起作用；网络参数应用于上下行数据，对主播、观众都起作用。实时通信场景，所有用户都有上下行数据，所以三部分参数对所有用户都起作用。

![](https://mc.qcloudimg.com/static/img/6dd38ad1b956cd1c885bfdbf1b2ca4ce/image016.png)

下面具体看下每部分参数的设置。
### 5.1 视频参数

![](https://mc.qcloudimg.com/static/img/263dff18fdaa2e01e1ff9f94bab43632/image018.png)


* 配置模式：提供预设的“标清”、“高清”、“超清”打包模式，选择后不需要再配置其他参数。建议选择“高清”。选择“自定义”模式，可以自己配置其他参数
* 编码格式：“自适应”由SDK根据设备性能和网络情况自行调整分辨率；“固定图像格式”选择一个固定的分辨率，提供4:3和16:9两种类型的分辨率。
* 编码码率：“自适应”由SDK根据设备性能和网络情况自行调整码率；“自定义”指定SDK可以调整的范围，如果需要固定码率可以把最大最小值设置成一样的
* 编码帧率：“自适应”由SDK根据设备性能和网络情况自行调整帧率；“自定义”指定一个期望的帧率。帧率和码率、清晰度相关，如果MinQP、MaxQP设置的不当，可能达不到期望的帧率。
* 冗余抗丢包：通过FEC等方式增加冗余度来抵消网络丢包，冗余度一般为丢包率的两倍。一般情况下建议关闭。

帧率、码率、分辨率有一定的相关性，QP设置的不合理也有可能会降低帧率。简单的用法可以直接选择预设的“标清”、“高清”、“超清”打包模式；自定义情况下，帧率、码率、分辨率的对应建议如下：

分辨率	| 码率	| 帧率
----	|----	|----
640 x 368 | 800Kbps | 25fps
960 x 540 | 1200Kbps | 15fps

### 5.2 音频参数

![](https://mc.qcloudimg.com/static/img/28a7f98d8d139042e5c9372e998333d3/image020.png)

* 配置模式：“默认”模式不需要再设置其他参数，“自定义”模式可设置更多参数。
* 音频场景：“开播”模式可以采集、编码、发送音频，适用于主播；“观看”模式不会打开音频设备也不会发送音频数据，适用于观众。
* 编码码率：设置音频码率，范围0~64
* 冗余抗丢包：通过FEC等方式增加冗余度来抵消网络丢包。互动直播场景建议关闭，实时通信场景建议打开。
* aec：回声消除。互动直播不连麦的场景建议关闭，互动直播可能连麦场景和实时通信场景建议打开。
* agc：自动增益。互动直播不连麦的场景建议关闭，互动直播可能连麦场景和实时通信场景建议打开。
* ans：噪声抑制。互动直播不连麦的场景建议关闭，互动直播可能连麦场景和实时通信场景建议打开。

### 5.3 参数差异

![](https://mc.qcloudimg.com/static/img/b38439c90daed4aaba9e8ae4a3b93367/image024.png)

不同平台、不同场景下的参数配置略有不同，根据页面显示的可配置选项配置即可。

如实时通信场景，音频参数和网络参数是不能配置的。

可配置参数可能会随着版本升级发生变化，以配置网页上显示的配置项为准。

# 三、客户端逻辑
## 1. 配置生效时机
在腾讯云上配置好后，客户端不会立即生效。客户端要在调用xxx api时，去后台拉取最新配置。拉取成功后会在本地保存。

## 2. 默认配置
SDK自带一套保底默认配置，用户可以调用的API修改保底默认配置，设置的参数可以从云端配置网站获得 ，参数值为明文json字符串。SDK使用配置时，如果云端配置第一次无法获取, 则使用保底默认配置。其他情况仍走之前云端配置逻辑。




