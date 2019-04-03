
## 概述

<p style="text-align:center;"> <img src="/image/tu1.png" class="sign"></p>

<p style="text-align:center;font-weight: bold;">
<a href="19.VersionRecord/README.md" style="color:#000000;">文档版本：V1.9.0</a>
</p>

<div id="Video_Tutorial">

<h3>视频</h3>

<p>为方便大家学习教程，每章节均提供视频与正文两种方式供大家选择浏览，后文不再赘述。</p>

<video width="100%"  controls   onclick="playPause()"    id="video" type="video/mp4" controlsList="nodownload" disablePictureInPicture src="http://uinvcenter.oss-cn-beijing.aliyuncs.com/DOCvideo/1.%E6%A6%82%E8%BF%B0.mp4" type="video/mp4" >
</video></div>

<script>
 function getCookie(name) {
            var strcookie = document.cookie;//获取cookie
            var arrcookie = strcookie.split(';');
            for(var i = 0; i< arrcookie.length;i++)
            var arr = arrcookie[i].split("=");
            if(arr[0] == name){
                return arr[1];
            }
            return "";
    }
    var myVideo = document.getElementById("video");
    var tokencookie =  getCookie('token');
    myVideo.addEventListener('play',function(){
        consoel.log(111)
        console.log(tokencookie);
        if(tokencookie != null ){
            // if(myVideo.paused){
                    myVideo.play();
                    console.log('你已经登陆了!')
            // }
        }else{
            console.log('你需要登录奥!')
        }
    });
</script>
### 正文

ThingJS 名称源于 物联网`Internet of Things (IoT)`中的 `Thing (物)`，意为面向物联网可视化开发的 `Javascript` 库。主要针对以一栋或多栋建筑所组成的园区级别的场景，可以应用于数据中心、仓储、学校、医院、安防、预案等多种领域。

下图清晰的反映了 ThingJS 在物联网领域中的定位：

<p style="text-align:center;"> <img src="image/procedure.png"></p>

ThingJS 基于 `HTML5` 和 `WebGL` 技术，可方便地在主流浏览器上进行浏览和调试，支持 PC 和移动设备。ThingJS 为可视化应用提供了简单、丰富的功能，只需要具有基本的 Javascript 开发经验即可上手。

ThingJS 提供了对场景的加载、分层级的浏览，对象的访问、搜索、以及对象的多种控制方式和丰富的效果展示，可以通过绑定事件进行各种交互操作，还提供了摄像机视角控制、点线面效果、温湿度云图、界面数据展示、粒子效果等等各种可视化功能。

更多功能展示，请参见：[在线开发](http://www.thingjs.com/guide/?m=sample)

综合demo展示，请参见：[综合Demo](http://www.thingjs.com/guide/?m=demo)

常见问题展示，请参见：[常见问题](16.CommonProblem/README.md)

版本更新内容，请参见：[版本记录](19.VersionRecord/README.md)

