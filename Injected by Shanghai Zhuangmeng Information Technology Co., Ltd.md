# Asset Fingerprint

Home improvement ERP management system
fofa grammar(https://fofa.info/)：
body="版权所有：上海装盟信息科技有限公司 400-021-8611"

![图片.png](https://cdn.nlark.com/yuque/0/2022/png/1976103/1666334222606-820c955c-8d16-44a6-87ce-a261e42d15a5.png#averageHue=%23071428&clientId=ue955b3aa-c2a4-4&crop=0&crop=0&crop=1&crop=1&errorMessage=unknown%20error&from=paste&height=82&id=u3cc9029b&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=103&originWidth=515&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9224&status=error&style=none&taskId=u582b2a4f-d089-4469-a53b-7c418d2e1ed&title=&width=412#averageHue=%23071428&crop=0&crop=0&crop=1&crop=1&id=VhjkF&originHeight=103&originWidth=515&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

# First

Due to the irregular settings of some webmasters, I obtained some source code and conducted a code audit on it. The cms is not open source, so I can only give some targeted source code

As shown in the figure, in lines 169-199, the parameter "userCode" is not filtered, and SQL is directly spliced and executed, resulting in SQL injection

![image.png](https://cdn.nlark.com/yuque/0/2022/png/1976103/1668478344746-e2537c54-18de-40ac-9f99-92ad2fe1448c.png#averageHue=%23fafaf9&clientId=ud0341bd1-66fd-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=700&id=ua8918851&name=image.png&originHeight=875&originWidth=1883&originalType=binary&ratio=1&rotation=0&showTitle=false&size=105984&status=done&style=none&taskId=u6e4d72a3-be0e-4f34-a566-f579b121147&title=&width=1506.4)

Later, I found out that the manufacturer that sells the CMS also has this kind of problem

page as shown

![image.png](https://cdn.nlark.com/yuque/0/2022/png/1976103/1668478452618-56c27d9a-e971-4c36-9caf-f095d19c1a29.png#averageHue=%23a6a9a4&clientId=ud0341bd1-66fd-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=411&id=ua2296252&name=image.png&originHeight=514&originWidth=934&originalType=binary&ratio=1&rotation=0&showTitle=false&size=239955&status=done&style=none&taskId=u6d6d269d-3d11-43fb-b9e1-04e61215bad&title=&width=747.2)

# process

There is an account login interface on the web side, and there are no loopholes in the normal test. We found that there is a WeChat applet in the scan code login

![图片.png](https://cdn.nlark.com/yuque/0/2022/png/1976103/1666331108058-15dcd14a-381d-4cea-a615-0274fb0430bc.png#averageHue=%23474746&clientId=ue955b3aa-c2a4-4&crop=0&crop=0&crop=1&crop=1&errorMessage=unknown%20error&from=paste&height=102&id=ua8d31859&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=128&originWidth=148&originalType=binary&ratio=1&rotation=0&showTitle=false&size=5203&status=error&style=none&taskId=ubb8582f1-78b2-488c-9ac2-1057d102038&title=&width=118.4#averageHue=%23474746&crop=0&crop=0&crop=1&crop=1&id=G3XDx&originHeight=128&originWidth=148&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

Then I found a small program on the mobile phone through WeChat search

![图片.png](https://cdn.nlark.com/yuque/0/2022/png/1976103/1666331385128-cd406098-e8d7-4e7f-87bb-d40ec822f333.png#averageHue=%234a4949&clientId=ue955b3aa-c2a4-4&crop=0&crop=0&crop=1&crop=1&errorMessage=unknown%20error&from=paste&height=192&id=ue72d9947&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=240&originWidth=105&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9567&status=error&style=none&taskId=ua5019712-448f-4283-9595-75872bc3632&title=&width=84#averageHue=%234a4949&crop=0&crop=0&crop=1&crop=1&id=UyA3J&originHeight=240&originWidth=105&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

There is also login on the mobile terminal, and the WeChat applet is captured through the triple linkage of charles+proxifier+burpsuite

[http://zminfo.erpjz.com:80/WEB_SERVICE/WeChatAPI_ERPMobile.ashx?type=LoginIndex&userCode=admin';WAITFOR](http://zminfo.erpjz.com:80/WEB_SERVICE/WeChatAPI_ERPMobile.ashx?type=LoginIndex&userCode=admin';WAITFOR) DELAY '0:0:5'--&passWord=1

![图片.png](https://cdn.nlark.com/yuque/0/2022/png/1976103/1666331465620-42f411d7-2f0a-4118-8cc5-b78be3bf4776.png#averageHue=%23f7f7f7&clientId=ue955b3aa-c2a4-4&crop=0&crop=0&crop=1&crop=1&errorMessage=unknown%20error&from=paste&height=439&id=u6beffec4&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=549&originWidth=1125&originalType=binary&ratio=1&rotation=0&showTitle=false&size=111482&status=error&style=none&taskId=ube14954c-febd-4ca0-8be5-7cddcad1faa&title=&width=900#averageHue=%23f7f7f7&crop=0&crop=0&crop=1&crop=1&id=I4CxV&originHeight=549&originWidth=1125&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

single quotes inject

![图片.png](https://cdn.nlark.com/yuque/0/2022/png/1976103/1666331516492-de237da8-1765-4121-b4ef-5ae47128a215.png#averageHue=%23f7f5f5&clientId=ue955b3aa-c2a4-4&crop=0&crop=0&crop=1&crop=1&errorMessage=unknown%20error&from=paste&height=460&id=u6cb677fe&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=575&originWidth=1167&originalType=binary&ratio=1&rotation=0&showTitle=false&size=120449&status=error&style=none&taskId=u94f946ec-3640-45da-a20b-d8c28408eec&title=&width=933.6#averageHue=%23f7f5f5&crop=0&crop=0&crop=1&crop=1&id=HUuzH&originHeight=575&originWidth=1167&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

It is found that the address of this applet is the same as the address of the web side, and the path is directly spliced

![image.png](https://cdn.nlark.com/yuque/0/2022/png/1976103/1668478766720-9770a6db-e717-45b5-8c4b-d7cb24a184f9.png#averageHue=%23fbf9f8&clientId=ud0341bd1-66fd-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=85&id=u2fa79504&name=image.png&originHeight=106&originWidth=931&originalType=binary&ratio=1&rotation=0&showTitle=false&size=52487&status=done&style=none&taskId=u3c48658b-a000-4330-84c0-ab6912014c6&title=&width=744.8)

Manual injection

![图片.png](https://cdn.nlark.com/yuque/0/2022/png/1976103/1666331671902-80f4de32-9612-4d6c-976a-9a6d5b7b60b8.png#averageHue=%23f9f8f8&clientId=ue955b3aa-c2a4-4&crop=0&crop=0&crop=1&crop=1&errorMessage=unknown%20error&from=paste&height=634&id=u66fc1e61&margin=%5Bobject%20Object%5D&name=%E5%9B%BE%E7%89%87.png&originHeight=792&originWidth=1582&originalType=binary&ratio=1&rotation=0&showTitle=false&size=161851&status=error&style=none&taskId=u4f560ff5-bf4d-48db-a25f-9c82dce80a7&title=&width=1265.6#averageHue=%23f9f8f8&crop=0&crop=0&crop=1&crop=1&id=ZRRtX&originHeight=792&originWidth=1582&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

Through sqlmap a lock dba permission osshell, whoami direct sys permission


