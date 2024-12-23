---
title: 为什么你应该保存好你的 Cookie
date: 2024-12-23 00:09:38
tags: 
    - 网络安全
    - Cookie
keywords: 
    - 网络安全
    - Cookie
categories: 技术
---

## 前言

这一阵子，风靡起统计华子的年度食堂消费情况，起因是这个库： [leverimmy/THU-Annual-Eat: 一年过去了，你在华子食堂里花的钱都花在哪儿了？](https://github.com/leverimmy/THU-Annual-Eat)。

不久后又出现一个网站 [2024 华子食堂消费总结](https://thu2024.food/)，似乎能更好的对数据进行展示，eg.

![](/imgs/watch-your-cookies/787caba4ea51d06ebb9e51b8425cd973.png)

正常人可能觉得：“Oh，好好玩”，于是就快乐地填写了学号和 Cookie……
但了解一点网安的人就该警惕起来了，在第三方网站上输入 Cookie 跟在第三方网站上填写密码没有区别啊！
F12 一看，好家伙有 Post 也不是本地处理的啊。好在是有开源的，姑且相信部署的是没有后门的版本吧。
（~~虽然我是不敢用的~~）

<!-- 但为了给不懂 Cookie 的重要性的人上一课，于是我只好当那个坏人了，于是悄悄部署了一份[有后门的版本](https://food.lesnow.top/)……

然后不到两个小时就得到了：

![](/imgs/watch-your-cookies/results.png)

WoW. 将近 100 条记录！看来大家的网络安全知识确实还欠佳啊。

> 不过以人格担保，虽然我保存了信息（只有消费记录，没有其他更敏感的个人信息），但绝对不会做坏事，只用来给大家展示 Cookie 的重要性，并将在这场小小网安实验后删除。(不信的话来 QQ 群 439149334 找群主对线)
> 大家不要模仿哦 ~ 也记得 Watch Your Cookies。 -->

## Cookie 泄露会导致什么？

**Cookie 代表了你的登录状态**。这也导致了 Cookie 泄露甚至比密码泄露还要严重，因为后者可能还会被两步验证之类的所保护。而很多情况下，拥有了 Cookie 就相当于拥有了登录的状态！

> 不过 Cookie 也经常用来储存别的信息，这里为了方便理解是有一点点表述上的偏差的。

虽然还没完全探索到底（期末太忙了），但初步探究就已经发现：
你清食堂消费这个案例中，`servicehall` **会泄露你的 姓名 照片 手机号 身份证号！！！**
也就是说 **完全开盒！！！**

> 不过 Cookie 是有 expires 时间的，`servicehall` 就有“会话”的生命周期，也就是说你关闭浏览器时它就没用了。
> 不小心填过 Cookie 的朋友们可以稍稍喘口气了 ~

![](/imgs/watch-your-cookies/expires.png)

所以，朋友们，保护好你们的 Cookies！
本地运行代码可以 check 一下代码是否会将 Cookie 等数据发送到奇怪的地方。
网站上除非十分自信没有后门，否则**千万不要输入你的 Cookie！**
如果网站是开源的，可以检查代码，然后部署你自己的实例，这样也相对安全。

更具体的科普视频 bilibili 就有很多，
比如 [Cookie、Session、Token究竟区别在哪？如何进行身份认证，保持用户登录状态？_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1ob4y1Y7Ep/)

太忙了不多写了，就让 GPT 继续回答一下吧。

## GPT 的回答

作为一名网络安全专家，我可以告诉你，**Cookie 泄露**是一个非常严重的安全问题，因为它可能导致用户的敏感信息被泄露、账户被劫持，甚至进一步的网络攻击。以下是对 Cookie 泄露风险的详细说明：

---

### **1. 什么是 Cookie？**
Cookie 是存储在用户浏览器中的小型数据文件，通常由网站创建，用于保存用户的会话信息、偏好设置以及其他数据。Cookie 的主要用途包括：
- **会话管理**：如用户的登录状态。
- **个性化设置**：如用户的语言偏好。
- **跟踪和分析**：用于广告和用户行为分析。

---

### **2. Cookie 泄露的常见风险**
当 Cookie 被恶意攻击者窃取时，可能导致以下风险：

#### **（1）会话劫持**
- **风险**：攻击者窃取用户的会话 Cookie（如登录状态的 Session Cookie），然后冒充用户访问网站。
- **后果**：攻击者可以直接登录用户账户，执行恶意操作，如转账、窃取敏感数据或更改账户设置。

#### **（2）身份盗用**
- **风险**：攻击者利用被窃取的 Cookie 模拟用户身份。
- **后果**：攻击者可以冒充用户在社交媒体、电子邮件或其他平台上进行恶意活动。

#### **（3）跨站脚本攻击（XSS）**
- **风险**：如果网站存在 XSS 漏洞，攻击者可以通过注入恶意脚本窃取用户的 Cookie。
- **后果**：攻击者可以通过 XSS 获取用户的会话 Cookie，从而劫持用户账户。

#### **（4）中间人攻击（MITM）**
- **风险**：如果用户在未加密的 HTTP 连接中传输 Cookie，攻击者可以通过网络嗅探工具拦截这些 Cookie。
- **后果**：攻击者可以使用这些 Cookie 模拟用户的身份，访问敏感信息。

#### **（5）第三方 Cookie 滥用**
- **风险**：某些第三方广告或分析脚本可能滥用 Cookie 数据，甚至被恶意利用。
- **后果**：用户的隐私数据可能被追踪或出售。

#### **（6）持久性 Cookie 泄露**
- **风险**：某些 Cookie 被设置为长期有效（如“记住我”功能的 Cookie），一旦泄露，攻击者可以长期利用这些 Cookie。
- **后果**：攻击者可能在很长一段时间内持续冒充用户。

---

### **3. Cookie 泄露的主要攻击途径**
以下是导致 Cookie 泄露的主要方式：

#### **（1）网络嗅探**
- 在未加密的 HTTP 连接中，Cookie 以明文形式传输，容易被攻击者拦截。

#### **（2）跨站脚本攻击（XSS）**
- 攻击者在受害者访问的网页中注入恶意脚本，通过 `document.cookie` 窃取用户的 Cookie。

#### **（3）跨站请求伪造（CSRF）**
- 攻击者利用用户的会话 Cookie，诱导用户执行未授权的操作。

#### **（4）不安全的存储**
- 如果 Cookie 被存储在用户设备上的不安全位置（如本地文件或不安全的浏览器扩展），可能被恶意软件窃取。

#### **（5）浏览器漏洞**
- 攻击者可能利用浏览器漏洞直接获取用户的 Cookie 数据。

#### **（6）社会工程攻击**
- 攻击者可能通过钓鱼攻击诱骗用户泄露 Cookie 数据。

---

### **4. 如何防范 Cookie 泄露？**
为了降低 Cookie 泄露的风险，可以采取以下措施：

#### **（1）使用 HTTPS**
- 确保网站启用了 HTTPS，所有 Cookie 数据在传输过程中都经过加密。

#### **（2）设置 Cookie 属性**
- **Secure 属性**：仅允许 Cookie 在 HTTPS 连接中传输。
- **HttpOnly 属性**：防止 JavaScript 访问 Cookie，减少 XSS 风险。
- **SameSite 属性**：限制跨站点请求使用 Cookie，防范 CSRF 攻击。

#### **（3）定期清理 Cookie**
- 用户可以定期清理浏览器中的 Cookie，减少长期有效 Cookie 被滥用的风险。

#### **（4）防范 XSS 攻击**
- 对用户输入进行严格验证和过滤，避免恶意脚本注入。
- 使用内容安全策略（CSP）限制脚本的执行来源。

#### **（5）防范中间人攻击**
- 用户应避免在公共 Wi-Fi 网络中访问敏感网站，或使用 VPN 加密流量。

#### **（6）减少 Cookie 数据存储**
- 仅在 Cookie 中存储必要的数据，敏感数据应存储在服务器端，而非客户端。

#### **（7）定期更新浏览器**
- 确保用户使用的是最新版本的浏览器，修复已知漏洞。

---

### **5. 总结**
Cookie 泄露可能导致严重的安全和隐私问题，包括账户劫持、身份盗用和敏感数据泄露。为了防范这些风险，网站开发者和用户都需要采取必要的安全措施，例如使用 HTTPS、设置安全的 Cookie 属性，以及防范 XSS 和中间人攻击。通过这些手段，可以有效降低 Cookie 泄露的风险，保护用户的隐私和数据安全。

如果你有更多关于网络安全的问题，随时可以向我咨询！