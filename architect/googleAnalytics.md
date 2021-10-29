## 设置

### 版本

* 谷歌统计分为新旧两个版本：Universal Analytics（旧版）、Google Analytics（分析）4   （新版）

* 以“UA-”开头的 ID，称为跟踪ID。只有旧版才有。新版有媒体资源ID（如：286341458） 和 衡量ID （G-K7WGMZQH67）

* ```
  Google Analytics（分析）4（以前称为“应用 + 网站”）是一项新型媒体资源，提供的报告与您在 Universal Analytics 媒体资源中看到的报告不同。Google Analytics（分析）4 媒体资源的优势之一是：您可以将其用于网站、应用，或同时用于这两者。Universal Analytics 媒体资源仅支持网站
  ```

* 说明UA仅支持网站衡量，新版支持应用衡量。

### 功能

#### 排除引荐功能

* 默认情况下，引荐来源会自动触发新会话。如果您排除了某个引荐来源，从已排除的网域来到您网站的流量就不会触发新会话（官方。即不会加入到统计）
* 设置：新版--数据流--网站--更多标记设置--多余的引荐流量。

## 报告

#### 流量获取 - direct / none

* 如果排除那些会带来流量的第三方网域，引荐来源仍将触发新会话，但该引荐来源网域的来源/媒介信息在报告中会显示为“(direct/none)（官方）
* direct / none 称为直接流量。谷歌统计通过 请求头 referer判断来源。如果referer为空，则为直接流量。
* <img src="https://www.yesharris.com/wp-content/uploads-webpc/uploads/2015/12/a0204.png.webp" alt="img" style="zoom:50%;" />

* 什么情况下是 direct / none：

  * 来源本身没有http referer。如：从word，excel等进入网页

  * 从手机app进入

  * 直接输入网址

  * http referer 传送失败

  * <img src="https://www.yesharris.com/wp-content/uploads-webpc/uploads/2015/12/a0207.jpg.webp" alt="img" style="zoom:50%;" />

    

  * ...

* 资料： [谷歌流量识别原理](https://www.yesharris.com/direct-traffic/)

* [几种流量介绍](https://cn.analyticsbook.org/google-analytics-traffic-sources/)

