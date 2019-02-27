---
date: 2017-06-06 23:06:19
status: public
title: WebQQ与聊天机器人的技术细节
keywords: 
- Python 
- QQ
- 聊天
- 机器人
tags:
- Python 
- QQ
- 聊天
- 机器人
categories: 好玩
 
---


# 登录模块
`class Login(HttpClient)`

1.  类初始化
```python
def __init__(self, vpath,qq_number=0,params=None):
    self.initTime = time.time()
    self.VPath = vpath  # QRCode保存路径
    self.UI_PTLOGIN2_URL = params.get('UI_PTLOGIN2_URL', '')
    self.QQ_LOGIN_URL =  params.get('QQ_LOGIN_URL')
    self.ClientID = params.get('ClinetID')
    self.PSessionID = params.get('PSessionID')
    self.QQ_GROUP_API_URL = params.get('QQ_GROUP_API_URL')
    self.REFERER = params.get('REFERER')
    self.MaxTryTime = params.get('MaxTryTime',5)

    AdminQQ = int(qq_number)

    # 1. 从 'http://w.qq.com/' get

    # 2. 从 UI_PTLOGIN2_URL = 'https://ui.ptlogin2.qq.com/cgi-bin/login?daid=164&target=self&style=16&mibao_css=m_webqq&appid=501004106&enable_qlogin=0&no_verifyimg=1&s_url=http%3A%2F%2Fw.own_qq_number.com%2Fproxy.html&f_url=loginerroralert&strong_login=1&login_state=10&t=20131024001' 获取登录页面（以w.qq.com为Referer头部）， 从login_html中获取APPID,SIGN（登录证书),JS_VERSION,MiBaoCss(?)

    # 3. 从login_html中获取mibao_css

    # 4. 开始时间 datetime.datetime.utcnow() ==》 millis

    # 5. 尝试MaxTryTime次：下载登录验证二维码，获取cookie，从QQ_LOGIN_URL = 'https://ssl.ptlogin2.qq.com/ptqrlogin?ptqrtoken={0}&webqq_type=10&remember_uin=1&login2qq=1&aid={1}&u1=http%3A%2F%2Fw.qq.com%2Fproxy.html%3Flogin2qq%3D1%26webqq_type%3D10&ptredirect=0&ptlang=2052&daid=164&from_ui=1&pttype=1&dumy=&fp=loginerroralert&action=0-0-{2}&mibao_css={3}&t=1&g=1&js_type=0&js_ver={4}&login_sig={5}&pt_randsalt=2' 登录，得到get的response，检查是否扫码（登录）
    #    `login_html = self.Get((self.QQ_LOGIN_URL).format(util.getQRtoken(QRSig), APPID, util.date_to_millis(datetime.datetime.utcnow()) - StarTime, MiBaoCss, JS_VERSION, SIGN),Refer=self.UI_PTLOGIN2_URL)`

    # 6. 扫码后删除二维码图片

    # 7. 记录登录账号的昵称

    # 8. 从cookie中得到PTWebQQ

    # 9. 先后post,get两个url，验证是否登录成功。

    # 10. 从response中获取VFWebQQ，MyUIN，并更新self.PSessionID

    # 11. 随机生成msgId，
```