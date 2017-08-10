# ren5 本地服务器搭建
 
环境 windows .

### 1 .red5 下载 

  http://red5.org/ 
  
### 2.解压到本地
 
 ### 3.双击 red5.bat 启动服务器 
 
 ### 4.运行起来后，就可以在浏览器里面输入http://localhost:5080/ 如果能打开red5的页面就说明已经运行起来了
 
 ### 5.安装demo ,和flash 播放器
 
 ### 6.修改index.html 
 
 用编辑器打开index.html，把rtmp那个播放器的脚本修改成下面的
 在这里面有两个直接协议的实现了，一个是RTMP，一个是RTMPT（是RTMP的变种，相当于RTMP用http包装后的协议）。 
点击那个播放的图标就可以播放流媒体了，但是要直播我们app的流还需要配置一点东西，在red5的根目录下打开webapps/oflaDemo这个目录
 用编辑器打开index.html，把rtmp那个播放器的脚本修改成下面的
 
 ```html
 <center>
<b>RTMP</b>
<div id='mediaspace'>This text will be replaced</div>
<script type='text/javascript'>
  jwplayer('mediaspace').setup({
    'flashplayer': 'player.swf',
    'file': 'test',
    'streamer': 'rtmp://192.168.1.102/oflaDemo',
    'controlbar': 'bottom',
    'width': '720',
    'height': '480'
  });
</script>
<br />

<b>RTMPT</b>
<div id='mediaspace2'>This text will be replaced</div>
<script type='text/javascript'>
  jwplayer('mediaspace2').setup({
    'flashplayer': 'player.swf',
    'file': 'BladeRunner2049.flv',
    'streamer': 'rtmpt://localhost:5080/oflaDemo',
    'controlbar': 'bottom',
    'width': '720',
    'height': '480'
  });
</script>
</center>

```
 
## 搭建 和直播参考自
[直播demo和服务器搭建](/red/red5.mhtml)
 
转自 博客 http://blog.csdn.net/u011485531/article/details/56013148
