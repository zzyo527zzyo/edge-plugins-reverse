# edge-plugins-reverse
# 一、 零基础浏览器插件逆向 🎀
&emsp;&emsp;今天🖐️🐟️的时候在玩浏览器插件，发现了一个可以更改浏览器主页的美图插件，用了一会觉得挺好用的，发现美中不足的是不能自定义图片，而且只能有六张图（👿插件都做了不做这个功能！！！）<br>
&emsp;&emsp;虽然没有接触过插件逆向，但是管他的直接冲，干就完事了☝😮<br>
&emsp;&emsp;所以有请今天的受害者:💙Anime Cute Girls HD Wallpaper New Tab💙<br>
![](./images/Pasted%20image%2020260213175958.png)
### 开始前的版本说明
&emsp;&emsp;浏览器：Microsoft Edge 🏃‍♀️
&nbsp;&nbsp;144.0.3719.115 (正式版本) (64 位)
&emsp;&emsp;下载地址：[Microsoft Update Catalog](https://www.catalog.update.microsoft.com/Search.aspx?q=edge&p=17)
### 开始
&emsp;&emsp;☝第一步下载该插件：<br>
&emsp;&emsp;☝[Anime Cute Girls HD Wallpaper New Tab - Microsoft Edge Addons](https://microsoftedge.microsoft.com/addons/detail/anime-cute-girls-hd-wallp/opikgkeiopokefaejegeghpfgmjajmah)<br>
&emsp;&emsp;接下来就要观察插件是储存在本地还是在☁️云端了：<br>
&emsp;&emsp;通过询问度娘和ai就知道了，浏览器插件的存储地址在：<br>
```
%LOCALAPPDATA%\Microsoft\Edge\User Data\Default\Extensions<br>
```
&emsp;&emsp;这说明！！！插件的存储地址是在本地的，那岂不是可以为所欲为，🤔为所欲为？？！<br>
![](./images/Pasted%20image%2020260213181714.png)<br>
&emsp;&emsp;那么这么多文件夹，哪一个是插件呢？？😭<br>
&emsp;&emsp;这时我们打开插件的详情信息，赫然发现浏览器的地址栏怎么有一个id呢☝😮<br>
![](./images/Pasted%20image%2020260213181910.png)
&emsp;&emsp;我们再将这个id和这个文件夹对比一下，发现一模一样！哦哦哦😮☝原来如此：<br>
&emsp;&emsp;opikgkeiopokefaejegeghpfgmjajmah这个就插件的文件夹名！太🀄了！<br>
&emsp;&emsp;我们现在打开文件夹那便是海阔凭鱼跃了，随便巡视领地了。<br>
&emsp;&emsp;经过几圈溜达，发现images文件夹里面不正是我们要找的图片吗？！！👌<br>
![](./images/Pasted%20image%2020260213182659.png)<br>
&emsp;&emsp;偷偷将想自定义的图片替换了image1.jpg，重新打开浏览器载入，却发现扩展已损坏😭😭😭我不活了<br>
![](./images/Pasted%20image%2020260213183050.png)<br>
&emsp;&emsp;怎么办🤔？这时我注意到图片的尺寸为19201080，会不会是我插入的图片尺寸问题？？？☝😮<br>

&emsp;&emsp;图像转换地址：[在线图片大小调整工具 - 免费调整和压缩图像尺寸](https://tool.xuecan.net/image-resize/)<br>
&emsp;&emsp;经过图像转换成相同像素重新载入🤔：结果还是此扩展已损坏！md😭😭😭我不活了<br>

&emsp;&emsp;怎么办🤔？这时我注意到metadata文件夹下面有两个json文件很可疑。hash.json？？验证内容.json？？<br>
![](./images/Pasted%20image%2020260213183834.png)<br>
&emsp;&emsp;难道说🤔这是签名校验？？打开文件夹一看有 "signature"和"file_hashes"字段心顿时凉了一半，亚麻咯🙅‍♀️这还搞个瘠薄<br>
&emsp;&emsp;😭😭😭<br>
&emsp;&emsp;😭😭😭<br>
&emsp;&emsp;😭😭😭<br>
&emsp;&emsp;这时我注意到扩展里面有个开发者模式，打开以后👉右边便多出来三个选项：加载解压缩的扩展？？！☝😮<br>
![](./images/Pasted%20image%2020260213184600.png)<br>
&emsp;&emsp;☝😮☝😮☝😮这不就是加载本地的插件吗？重新下载完好的插件，再将自定义的图片替换image1，将整个文件夹放到桌面，直接加载！！！<br>
&emsp;&emsp;此处注意应该加载含manifest清单文件的父文件夹，不然会加载失败<br>
![](./images/Pasted%20image%2020260214173747.png)<br>
&emsp;&emsp;此时我们就成功更换图片了！！！🍓<br>
&emsp;&emsp;我们直接更改文件夹插件直接失效，👀采用本地加载的方式成功了<br>
&emsp;&emsp;这说明什么？这说明之前加载失败并不是本地插件内部文件的签名校验，而是浏览器的云端校验☝😮<br>

&emsp;&emsp;那么新的问题来了，如果我们想多添加几张照片怎么办呢？<br>
&emsp;&emsp;观察力👍强的人就会在之前的操作中发现，index.html文件📃就明晃晃地在images文件的同级目录下<br>
&emsp;&emsp;实在找不到直接搜索🔍整个文件夹的html文件也行<br>
&emsp;&emsp;这时我们就定位到了页面的文件，使用自己的代码编辑器（这里我用的android stuido）打开我们可以发现这里的src明显指向了我们之前修改图片的文件夹📂<br>
![](./images/Pasted%20image%2020260214174553.png)<br>
&emsp;&emsp;显然根据mobile我们就知道下面的几张图片是适配移动端的，所以我们要修改的是上面的👆<br>
&emsp;&emsp;我们直接按照他的格式在div中新增<br>
```
<img id="background6" src="imgs/image7.jpg">
```
&emsp;&emsp;一行，并在文件夹里面添加image7图片<br>
&emsp;&emsp;这里我们只是修改了前端页面，之前在使用插件过程中我们明显可以👌感觉到，插件有一个点击切换图片的功能，这说明我们还需要寻找定位js中的点击功能☝😮<br>
&emsp;&emsp;我们进入js文件夹，毫不费力的就看到了这个可疑的background.js文件📃<br>
![](./images/Pasted%20image%2020260214175423.png)<br>
&emsp;&emsp;输入background或者image关键词你就可以👌轻松定位到这里<br>
&emsp;&emsp;用代码编辑器打开该文件<br>
![](./images/Pasted%20image%2020260214175627.png)<br>
&emsp;&emsp;同理我们仿照他的格式新增一行（此处需要注意使用ctrl+s保存修改的代码才会生效）<br>
```
elemenetGetId('background6').onclick = function () {  
chrome.storage.local.set({ 'picUrl': "'imgs/image7.jpg'" });  
elemenetGetId('background').style.backgroundImage = 'url("imgs/image7.jpg")';  
}
```
![](./images/Pasted%20image%2020260214180100.png)<br>
&emsp;&emsp;这里我们看见六张图片变成了七张，这说明修改成功了！！！<br>
## 关于

### bug反馈

✅983821691@qq.com

		
### ---本软件不参与任何商业行为

声明：本仓库仅用于存储软件，不参与任何商业行为，仅供学习交流使用，如有侵权，请联系本人删除。

## Star History

<a href="https://star-history.com/#zzyo527zzyo/edge-plugins-reverse&Date">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=zzyo527zzyo/edge-plugins-reverse&type=Date&theme=dark" />
    <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=zzyo527zzyo/edge-plugins-reverse&type=Date" />
    <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=zzyo527zzyo/passjun&type=Date" />
  </picture>
</a>
