# Gmail Search

跨平台（macOS / Windows）邮箱搜索桌面应用。支持多账号、Gmail 搜索语法、标签 / 文件夹筛选、邮件正文查看、附件下载、发票批量下载。对 Gmail 仅申请**只读**权限（`gmail.readonly`），不会修改或删除你的邮件。

---

## 一、安装（Windows）

1. 从本仓库 **Releases** 页面下载最新的 `Gmail Search Setup x.x.x.exe`。
2. 双击安装。若弹出蓝色提示「Windows 已保护你的电脑」——因为安装包未购买代码签名证书，属正常现象——点 **「更多信息」→「仍要运行」**。
3. 按向导完成安装，会创建桌面快捷方式「Gmail Search」，完成后自动启动。

> 之后有新版本时，应用启动会**自动提示更新**，点确认即可下载安装，无需再手动下载。

## 二、首次配置：Google OAuth 凭据（约 5 分钟，一次性）

要登录 Gmail，需要你自己创建一套 Google OAuth 凭据：

1. 打开 <https://console.cloud.google.com>，登录并新建一个项目（名字随意）。
2. 「API 和服务 → 库」，搜索 **Gmail API**，点「启用」。
3. 「API 和服务 → OAuth 同意屏幕」：User Type 选 **External**，填应用名和你的邮箱；在「测试用户」中加入你要登录的 Gmail 地址。
4. 「API 和服务 → 凭据 → 创建凭据 → OAuth 客户端 ID」，应用类型选 **桌面应用**，记下 **Client ID** 和 **Client Secret**。
5. 打开应用，在设置面板粘贴 Client ID / Client Secret 并保存。凭据只保存在本机。

## 三、添加邮箱账号

### Google（Gmail / Workspace）

点「＋账号 → Google 账号」，系统浏览器会打开 Google 登录页：

- 电脑浏览器已登录该账号：直接点确认即可；
- 未登录：可在登录页选「用其他设备登录 / 通行密钥」，Google 会显示二维码，用已登录 Gmail App 的**手机扫码**确认，无需在电脑输密码。

授权成功后应用保存令牌，之后无需重复登录。

### 其他邮箱（IMAP / POP3 密码登录）

点「＋账号 → 其他邮箱」，选协议，填邮箱、密码和服务器地址。优先选 **IMAP**（支持文件夹和服务器端搜索）；POP3 只有收件箱，且只能按邮件头（发件人 / 收件人 / 主题 / 日期）本地搜索，不支持正文搜索。

常见服务器（POP3 把 `imap` 前缀换成 `pop`，端口 995）：

- QQ 邮箱：`imap.qq.com`（需在 QQ 邮箱设置里生成「授权码」当密码）
- 163 邮箱：`imap.163.com`（同样需授权码）
- IONOS 托管域名（如 flyquipe.com）：`imap.ionos.fr`

密码经系统加密（macOS 钥匙串 / Windows DPAPI）后仅保存在本机。

## 四、搜索语法

搜索框支持 Gmail 搜索语法，例如：

- `from:boss@example.com` 某人发来的
- `subject:发票 has:attachment` 主题含「发票」且有附件
- `after:2026/1/1 before:2026/7/1` 时间范围
- `filename:pdf larger:5M` 大于 5MB 的 PDF 附件

默认只搜索最近 3 个月（可在设置里改，`0` = 不限）；查询里自己写了 `after:` / `before:` 时以你的条件为准。

> IMAP / POP3 账号支持 Gmail 语法的子集：`from:` `to:` `subject:` `after:` `before:` `larger:` `smaller:` `is:unread` `is:starred` 及正文关键词。

## 五、批量下载发票

点搜索栏的「⬇ 发票」，选时间范围，命中邮件里的 PDF 附件会按开票方归类保存，文件名以邮件日期为前缀；已下载过的邮件自动跳过，不会重复。

- Windows 保存位置：`C:\Users\<用户名>\Downloads\factures\`

## 数据与隐私

- 所有凭据（Gmail 授权令牌、IMAP / POP3 密码）都经操作系统加密（macOS 钥匙串 / Windows DPAPI）后保存在**本机**，不上传。
- 对 Gmail 仅申请**只读**权限。
- 邮件正文安全渲染，屏蔽邮件里的脚本和远程跟踪像素。
- 各台电脑独立配置：换电脑需重新粘贴 OAuth 凭据、重新授权账号、IMAP / POP3 重新输一次密码。
