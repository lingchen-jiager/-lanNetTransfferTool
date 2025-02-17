# 局域网文件及文本传输工具（网页版）

## 简介
本项目基本上是由cursor的claude sonnet模型自动生成的，我的250条免费额度用完了，目前做到了可用的程度。
能够实现局域网内文件和文本的传输。自动适配了电脑端和移动端。
仍有一些bug，会在后文说明，我本身没有系统学过flask和前端知识，所以基本所有代码都是由cursor生成，到了后期代码多了之后，自己的知识不够用，只依赖cursor修改起来就力不从心了，
我把这个小工具开源出来，本项目很简单，核心只有index.html、app.py、main.js三个文件，可以供初学者学习练手参考。当然也可以部署到局域网或者公网使用，基本功能已经实现，剩下的就是修改完善了。
或者有前端和flask基础的朋友们感兴趣也可以用cursor优化一下，让这个小项目成为一个更完善的初学者练手项目，毕竟学习编程，自己做出一个可用的工具来还是有正向激励作用的。
### 截图
![image](https://github.com/user-attachments/assets/5919fbf0-6722-4e31-8ce8-479a6de15838)

![image](https://github.com/user-attachments/assets/440670bb-e13c-44d0-9663-74b1055e9078)


![image](https://github.com/user-attachments/assets/fbe100b3-fa45-438c-83cd-ba1aebb00205)

详细说明：

## 文件结构：
```txt
项目根目录/
├── app.py                 # Flask主应用文件
├── devices.json           # 设备信息存储文件
├── templates/             # 模板目录
│   └── index.html        # 主页模板
├── static/               # 静态文件目录
│   ├── css/             # CSS文件
│   └── js/              # JavaScript文件
|── ── ──
```
## 使用
```cmd
python app.py
```
本项目开发环境为python3.10.0版本，过低版本可能无法运行，请悉知。
在app.py路径下打开cmd窗口，运行上述命令即可。
当前代码为局域网下运行的版本，无需更改即可用。
如需部署到公网，需要使用宝塔面板申请ssl证书，然后修改app.py中部分代码并在反向代理配置时，按照上述nginx配置文件配置。

## 目前实现功能：

1. 局域网内设备互相传输文件。（通过ip判定，ip相同则判定为同一个局域网内的设备，所以不能使用代理ip）
2. 局域网内设备互相发送消息。
3. 文件下载路径默认为浏览器默认下载路径，无法更改。

## 目前已知的bug如下：
1. 文件传输不快，建议传输小文件，速度大概在2MB/s以内，应该是cursor的传输代码有待于优化，由于我不懂js，不咋会优化，所以能用就可以了，感兴趣的朋友可以优化一下文件传输部分。
2. 接收端只能同时接收一个文件，且没有接收确认的机制，所以如果出现B、C设备同时向A设备发送文件的情况，就会出错。
3. 由于谷歌浏览器会杀后台，所以在谷歌浏览器传输时一旦网页处于后台状态，则传输速度会极大降低到几KB/s。
4. 无法使用cloudflare的代理功能，由于使用同一个公网ip来判定是否属于同一个局域网，所以如果使用cloudflare的dns中的代理（这样你的服务器ip就被隐藏了，减少一部分攻击），则每次用户访问网页，服务器端读取到的都是cloudflare的ip地址，无法识别到真实ip，也就识别不出同一个局域网内的设备。
