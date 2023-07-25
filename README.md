# Short-Link
## 1. 什么是短网址/短链接?
* 短链接, 通俗来说是将比较长的URL网址, 通过程序计算等方式, 转换为简短的网址字符串
* eg: 
  * 百度: dwz.cn
  * 微博: t.cn
  * ...

### 2. 为什么要使用短网址/短链接?
* 公司内部有很多需要发送链接的场景, 业务侧的链接通常会比较长, 在发送短信、IM工具发送消息、push等场景下长链接有以下劣势：
  1. 短信内容超长， 1条消息被拆分成多条短信， 浪费钱
  2. 微博等平台有字数限制
  3. 飞书、钉钉等IM工具对长链接（带特殊符号的）识别有问题
  4. 短链接转成二维码更清晰
 
## 3. 短网址/短链接需求拆解
根据需求分析, 可以将需求拆分为**转链模块, 存储和访问模块**
* 转链模块
  1. 多个相同的长链转短链请求, 都被转为同一个短链
  2. 生成的短链为尽量短的字符
  3. 屏蔽一些侮辱性词汇和特殊含义类词汇, eg:f**k, stupid, version ...
  4. 避免循环转链(把已经是短链的再拿来转短链)
* 存储模块
  1. 保存原始长链接和短链接的对应关系
  2. 能够根据短链接查找到原始的长链接
* 查看链接模块
  1. 根据短链接查询到长链后返回重定向响应
  2. 后续数据报表需求可能需要采集并统计请求头数据

## 系统设计
* 总体设计方案
  * 短链接项目肯定是读多写少，数据写入后基本不会改变，可以放心使用Redis缓存（不需要考虑数据一致性问题）提高系统效率；

  * 转链功能
    长链接进入 -> 使用发号器获得长链接对应的递增序号 -> 根据需要转换成62进制的数（乱序 + 加密 => 短域名） -> 根据短域名生成短链->返回短链；
    * 存储短链功能
    * 根据短链重定向功能
    * 短链生成方式
   
... ...
  
