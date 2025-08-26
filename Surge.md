# Surge

## 问题

我遇到的：

- 订阅变更，规则、策略手动维护麻烦

网友说可以：

- 基础功能
  - 订阅汇总
  - 订阅储存
  - 订阅同步
  - 订阅转换 (适配不同代理工具)
  - 本地节点转订阅
  - 节点过滤/整理/重命名/去重
  - 基于 gist 的文件管理、同步
- 对节点进行脚本操作
  - 节点的解锁测试
  - 节点入口落地检测
  - 节点测速
  - UDP检测
  - 利用Cloudflare对节点进行裂变/优选等
  - ~抓取Telegram频道中的节点~

## 自定义策略组与分流规则

### 安装 Sub-Store

- 官方默认版模块(支持 App 内使用编辑参数): [`https://raw.githubusercontent.com/sub-store-org/Sub-Store/master/config/Surge.sgmodule`](https://raw.githubusercontent.com/sub-store-org/Sub-Store/master/config/Surge.sgmodule)
- Surge / More / Module / Install from URL...
- 订阅成功后，从模块中选择启用
- 解密 / 升成新证书 / 将证书安装到系统 / 启用 HTTPS 解密 (Decrypt / Generate New Certificate + Install to System + MitM Over HTTP/2 / Enable HTTPS Decryption) (macOS 证书管理通过 KeyChain Access)
- 重启 Surge，并启用系统代理

### 使用 Sub-Store

- 浏览器访问 [https://sub.store](https://sub.store)，网页正常打开并且未弹出任何错误提示，说明 Sub-Store 已经配置成功
- 在 Sub-Store 按引导创建订阅
- 点击列表项“空白区域"打开「预览/拷贝订阅」面板，复制「Surge(macOS)」订阅链接，格式为 `https://sub.store/download/<NAME>?target=SurgeMac`
- 全局替换 [X.conf](./X.conf) 配置文件中“订阅地址"字符为 Sub-Store 创建的订阅链接
- Surge 导入此配置文件、勾选，完成配置

### 排错指南

- 服务 [https://sub-store.vercel.app](https://sub-store.vercel.app) 搭建在 Vercel 上, 模块和脚本下载，需要代理访问
- 浏览器中访问 [https://sub.store/api/utils/env](https://sub.store/api/utils/env) (注意是 HTTPS 协议) 应该可以看到版本号
- 如果报错, 尝试访问 [http://sub.store/api/utils/env](http://sub.store/api/utils/env) (注意是 HTTP 协议) 如果成功，说明是 MitM/证书信任的问题

### 物料

- [sub-store-org/Sub-Store: Advanced Subscription Manager for QX, Loon, Surge, Stash, Egern and Shadowrocket!](https://github.com/sub-store-org/Sub-Store)
- [rename.js](https://github.com/Keywos/rule/blob/main/rename.js)
- [xream/sub-store - Docker Image | Docker Hub](https://hub.docker.com/r/xream/sub-store)
- [deezertidal/Surge_Module: Surge 模块/脚本/规则/分流/破解/解锁](https://github.com/deezertidal/Surge_Module?tab=readme-ov-file)，规则可取
- [szkane/ClashRuleSet](https://github.com/szkane/ClashRuleSet)，规则可取
