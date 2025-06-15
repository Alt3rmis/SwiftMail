# SwiftMail

SwiftMail 是一个基于 Swift 和 Vapor 框架的邮件发送组件，提供了简单易用的 API 来发送电子邮件。

## 功能特点

- 支持 SMTP 邮件发送
- 支持 HTML 和纯文本邮件内容
- 支持附件发送
- 支持抄送和密送
- 支持自定义邮件头
- 完全异步操作
- 基于 Vapor 框架，性能优异

## 系统要求

- Swift 5.7+
- Vapor 4.0+
- macOS 12.0+ / Ubuntu 20.04+

## 安装

### Swift Package Manager

在您的 `Package.swift` 文件中添加以下依赖：

```swift
dependencies: [
    .package(url: "https://github.com/yourusername/SwiftMail.git", from: "1.0.0")
]
```

## 使用方法

### 基本配置

```swift
import SwiftMail

// 配置邮件服务器
let mailConfig = MailConfig(
    hostname: "smtp.example.com",
    port: 587,
    username: "your-email@example.com",
    password: "your-password",
    secure: .tls
)

// 创建邮件客户端
let mailClient = MailClient(config: mailConfig)
```

### 发送简单邮件

```swift
// 创建邮件
let email = Email(
    from: "sender@example.com",
    to: ["recipient@example.com"],
    subject: "测试邮件",
    body: "这是一封测试邮件"
)

// 发送邮件
try await mailClient.send(email)
```

### 发送 HTML 邮件

```swift
let email = Email(
    from: "sender@example.com",
    to: ["recipient@example.com"],
    subject: "HTML 测试邮件",
    body: """
    <html>
        <body>
            <h1>Hello World</h1>
            <p>这是一封 HTML 格式的测试邮件</p>
        </body>
    </html>
    """,
    contentType: .html
)
```

### 发送带附件的邮件

```swift
let attachment = Attachment(
    filename: "document.pdf",
    contentType: "application/pdf",
    data: Data(contentsOfFile: "path/to/document.pdf")
)

let email = Email(
    from: "sender@example.com",
    to: ["recipient@example.com"],
    subject: "带附件的邮件",
    body: "请查看附件",
    attachments: [attachment]
)
```

## 错误处理

```swift
do {
    try await mailClient.send(email)
} catch MailError.connectionFailed {
    print("连接邮件服务器失败")
} catch MailError.authenticationFailed {
    print("认证失败")
} catch {
    print("发送邮件时发生错误：\(error)")
}
```

## 贡献

欢迎提交 Pull Request 和 Issue！

## 许可证

MIT License