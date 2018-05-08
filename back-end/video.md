基本术语

DRM: Digital Rights Managment, 通过加密手段防止视频被非法播放

HLS: \(HTTP Live Streaming\). Based on HTTP, for Apple specific

* HLS presentation consists of media segments that contain audio, video, subtitles, or a multiplex of both audio and video. 
  Media segment URLs
   are referenced from media playlists \(a text-based format, usually stored in files with the .m3u8 file extension\).
* Use MPEG2 TS\(Transport Stream\) format. Normally, we use MP4 format, to convert it to MPEG2 TS which can be played as Live streaming.
* the media files may be encrypted

MPEG DASH Adaptive Streaming. Based on HTTP, for other browsers \(except for apple\)

* an MPEG DASH presentation consists of an initial XML manfifest, called the Media Presentation Document \(MPD for short\), which describes media segments that form a complete presentation
* tutorial: [https://www.bento4.com/developers/dash/](https://www.bento4.com/developers/dash/)

RTMP \(Real Time Messaging Protocol\) cannot be used on webpage directly. Use to serve Flash

ffmpeg

* crop videos:P downgrade resolution
  * ffmpeg -i inputfile.avi -croptop 88 -cropbottom 88 -cropleft 360 -cropright 360 outputfile.avi
* tutorial: [http://keycorner.org/pub/text/doc/ffmpeg-tutorial.htm](http://keycorner.org/pub/text/doc/ffmpeg-tutorial.htm)

Tools

* mp4hls: mp4 to hls. Based on mp42hls. one or more MP4 files to a multi-bitrate HLS master playlist
  * tutorial: [https://www.bento4.com/developers/hls/](https://www.bento4.com/developers/hls/)
* mp42hls: single MP4 file to single-bitrate HLS presentation
* mp4dash: convert one or more input media files into a complete MPEG DASH presentation
  * related tools:
    * mp4fragment: the input of mp4dash has to be fragmented first
    * mp4info: show whether an mp4 file is fragmented or not

直播推送协议比较

* RTMP：

  优点 CDN 支持良好，主流的 CDN 厂商都支持 协议简单，在各平台上实现容易 缺点 基于 TCP ，传输成本高，在弱网环境丢包率高的情况下问题显著 不支持浏览器推送 Adobe 私有协议，Adobe 已经不再更新

* WebRTC

  优点 W3C 标准，主流浏览器支持程度高 Google 在背后支撑，并在各平台有参考实现 底层基于 SRTP 和 UDP，弱网情况优化空间大 可以实现点对点通信，通信双方延时低 缺点 ICE,STUN,TURN 传统 CDN 没有类似的服务提供

七牛云

* 延迟优化： [http://blog.qiniu.com/archives/6996](http://blog.qiniu.com/archives/6996)
* 性能测试 [http://blog.qiniu.com/archives/7229](http://blog.qiniu.com/archives/7229)
  * 影响视频清晰度的指标
    * 帧率
    * 码率
    * 分辨率
    * 量化参数（压缩比）
  * 影响视频流畅度
    * 码率
    * 帧率
* 实践 [http://blog.qiniu.com/archives/7362](http://blog.qiniu.com/archives/7362)

* Other

  * 阿里直播： [http://www.infoq.com/cn/articles/alibaba-broadcast-platform-technology-challenges](http://www.infoq.com/cn/articles/alibaba-broadcast-platform-technology-challenges)
  * tutorial [https://www.dacast.com/tutorials-on-live-streaming-and-video-hosting/](https://www.dacast.com/tutorials-on-live-streaming-and-video-hosting/)



