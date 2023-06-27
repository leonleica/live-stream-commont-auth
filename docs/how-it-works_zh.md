# live-stream-comment-auth 直播弹幕认证是如何工作的？
[English](how-it-works.md) | 简体中文
## 核心概念

直播弹幕认证的原理是捕获直播平台上已注册用户发送的信息。该信息必须具有表示特定用户的唯一用户ID（uid）。

例如，bilibili直播中的弹幕具有良好的身份验证数据结构。它包括bili用户的uid和一个20个字符的空间来传递消息。如果用户想登录到第三方平台，我们可以向用户发送一个20个字符的验证码，然后用户应该将其发送到选择的bilibili直播间作为弹幕。因此，我们会通过弹幕机捕获弹幕消息。消息包含了buid和验证码。

## 用户如何登录或注册？

1. 用户从第三方平台请求验证码，我们称之为“vcode”。
2. 用户打开bilibili直播间并将vcode作为弹幕发送。
3. 直播弹幕认证工作程序捕获弹幕并检查vcode是否有效。
4. 如果vcode有效，则工作程序将向第三方平台发送JWT令牌。
5. 用户可以使用JWT令牌登录第三方平台。