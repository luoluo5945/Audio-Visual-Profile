完成这个令人兴奋的玩意，其实得益于html5的Audio API（https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Audio_API）<br>
Web Audio API 提供了在Web上控制音频的一个非常有效通用的系统，允许开发者来自选音频源，对音频添加特效，使音频可视化，添加空间效果 （如平移），等等。
说白了就是一个处理音频的对象（AudioContext），封装了一系列的针对音频文件的方法。
<br><br>
首先，我们先来总结一下实现音频可视化的大概流程（我先说的直白点，方便新手上路，代码中注释非常详细，这里算是大致介绍一下思路）<br>
（一） 获取上传的音频文件（通过input的files就可以获取）<br>
（二）对文件进行解码，通过fileReader.readAsArrayBuffer(file)读取文件，fileReader.onload是这个函数的回调。
注：解码后的得到的是一个二进制的数据，为什么要解码，因为AudioContext这个对象只能读取二进制的数据，不能直接读取file。解码过程需要一定时间，大概
几秒，最好做个定时器或者loading之类的，让人能感知到。<br>
（三）解码成功后的文件e.target.result，要对这个二进制的文件进行分析，AudioContext已经封装了分析方法，分析完了把所有的节
点连接起来，进行播放<br>
（四）因为到这步已经获取了分析后的音频数据（数组），通过canvas的requestAnimationFrame还有最终的音频数组，循环画出音频的图形。
