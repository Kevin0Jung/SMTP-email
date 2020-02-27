# SMTP(Simple Mail Transfer Protocol)

Created: Feb 23, 2020 10:45 AM
Tags: 服务器, 网络, 邮件

## 邮件的收发过程

一般情况下，一封邮件的发送和接收过程如下。

**1)** 发信人在用户代理里编辑邮件，包括填写发信人邮箱、收信人邮箱和邮件标题等等。

**2)** 用户代理提取发信人编辑的信息，生成一封符合邮件格式标准（RFC822）的邮件。

**3)** 用户代理用SMTP将邮件发送到发送端邮件服务器（即发信人邮箱所对应的邮件服务器）。

**4)** 发送端邮件服务器用SMTP将邮件发送到接收端邮件服务器（即收信人邮箱所对应的邮件服务器）。

**5)** 收信人调用用户代理。用户代理用POP3协议从接收端邮件服务器取回邮件。

**6)** 用户代理解析收到的邮件，以适当的形式呈现在收信人面前。

## SMTP协议

SMTP是英文Simple Mail Transfer Protocol的缩写，意为简单邮件传输协议，默认端口为25

在SMTP协议中，电子邮件由三部分组成，信封、首部和正文。

- 信封

      信封包括发信人的邮件地址和接收人的邮件地址，用两条SMTP命令指明。

① MAIL FROM:<发信人的地址>，告诉SMTP服务器发信人的地址。

② RCPT TO:<收信人的地址>，告诉SMTP服务器收信人的地址。

- 首部

    首部中常用命令：

    ① FROM：<姓名><邮件地址>，表明邮件发送者是谁。

    ② TO：<姓名><邮件地址>，表明邮件接收者是谁。

    ③ SUBJECT：<邮件标题>，表明邮件的主题。

    ④ DATE：<时间>，表明发邮件的时间。

    ⑤ REPLY-TO：<邮件地址>，表明邮件的回复地址。

    ⑥ Content-Type：<邮件类型>，表明邮件包含文本、HTML超文本和附件的哪些类型。

    ⑦ X-Priority：<邮件优先级>，表明邮件的发送优先级。

    ⑧MIME-Version：<版本>，MIME的意思是Multipurpose Internet Mail Extensions，即多用途Internet邮件扩展标准，它对传输内容的消息、附件及其他的内容定义了格式。

- 正文

    正文是邮件的内容。首部以一个空行结束，再下面就是正文部分。

- 结束符号

    邮件以“.”结束。

### SMTP邮件传输共三个阶段：

1. 建立SMTP连接
2. 数据库之间传输
3. 连接关闭

 在步骤1中建立SMTP连接也就是通过[TCP](https://www.notion.so/TCP-IP-c2d706c754804279b81986e598df8d01)三次握手进行通讯

## 通信过程

一个具体的SMTP通信（如发送端邮件服务器与接收端服务器的通信）的过程如下：

1. 发送端邮件服务器（以下简称客户端）与接收端邮件服务器（以下简称服务器）的25号端口建立[TCP](https://www.notion.so/TCP-IP-c2d706c754804279b81986e598df8d01)连 接。
2. 客户端向服务器发送各种命令，来请求各种服务（如认证、指定发送人和接收人）。
3. 服务器解析用户的命令，做出相应动作并返回给客户端一个响应。
4. 2和3交替进行，直到所有邮件都发送完或两者的 连接被意外中断。

![https://image.3001.net/images/20181102/1541138032_5bdbe6705cf6a.png](https://image.3001.net/images/20181102/1541138032_5bdbe6705cf6a.png)

# 使用SMTP发送邮件的Python实现
1. ### 建立连接
 发送端邮件服务器与接收端邮件服务器的25号端口建立TCP连 接。
```python
    smtp = smtplib.SMTP()
    smtp.connect('smtp.**.com', '25')
    smtp.login('username@**.com','password')
```
2. ### 数据之间传输
	从发件人对应的SMTP服务器传输到收件人服务器
```python
    smtp.sendmail('username@**.com', 'adressee@**.com', msg.as_string())
```
3. ### 传输结束
```python
    smtp.quit()
```
## 实践结果：

<img src="C:\Users\kevin\Desktop\smtp.png" alt="smtp" style="zoom:60%;" />

