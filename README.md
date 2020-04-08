# VR_Video-Play

> 万能播放器

## 特性

- 支持 x86 cpu arm 架构；
- Android 基于：FFmpeg + OpenSL + OpenGL + Mediacodec 的视频播放 SDK，可播放网络、本地和广播等流媒；
- 支持播放VR360度全景视频
  - 1、支持当前播放页直接切换播放源；
  - 2、优先选用 GPU 解码，解码速度更快；
  - 3、支持软解码和硬解码；
  - 4、直接用 mediacodec 解码 avpacket 数据；
  - 5、支持用于传统直播和VR直播；
  - 6、底层使用 FFmpeg 解码支持各种格式的音视频播放；
  - 7、支持 rtmp, http, hls 等多种流媒体协议。

# Demo预览

<p align="center">
 <img src="image/a.gif" style="width: 50%"/>
 <img src="image/b.gif" style="width: 50%"/>
</p>

+ 播放传统视频

```Java
  private WLPlayer wlPlayer;
  private GlSurfaceView glSurfaceView;
  //初始化
  glSurfaceView=findViewById(R.id.wlglsurfaceview);
  wlPlayer=new WLPlayer();
  wlPlayer.setWlOnParparedListener(new WlOnParparedListener() {
              @Override
              public void onParpared() {
                  System.out.println("播放");
                  wlPlayer.start();
              }
          });
  wlPlayer.setGlSurfaceView(glSurfaceView);
    //播放
  wlPlayer.setSource("http://vfx.mtime.cn/Video/2019/03/21/mp4/190321153853126488.mp4");
  wlPlayer.start();
```

+ 播放 VR 视频

```Java
        private GlSurfaceView glSurfaceView;

        private VrSurfaceView vrSurfaceView;

         //初始化
        vrSurfaceView=findViewById(R.id.play_vr_glsv);
        player=new WLPlayer();
        player.setWlOnParparedListener(new WlOnParparedListener() {
            @Override
            public void onParpared() {
                MyLog.d("开始播放----");
                System.out.println("播放");
                player.start();
            }
        });

         player.setOpenVr(true);   //设置成播放VR视频
         player.setVrSurfaceView(vrSurfaceView);
         player.setSource(VIDEO_URL);
         player.start();
```

**注意！传统视频是用 GlSurfaceView, 而 VR 视频是用 VrSurfaceView 显示**

## 播放器API

```Java
 public void parpared() //异步开始准备播放，成功后会回调WlOnPreparedListener接口
 public void start()  //开始播放
 public void pause()  //暂停
 public void resume();//暂停后恢复播放
 public  void stop() //停止播放释放资源
 public void seek(int sedc) //进度条拖动
 public void setGlSurfaceView(GlSurfaceView glSurfaceView) //设置平面显示的surface
 public void setVrSurfaceView(VrSurfaceView vrSurfaceView) //设置VR显示的surface
 public void setOpenVr(boolean openVr) //设置是否打开VR模式
 public void setSource(String source) //设置播放源
 public void playNext(String url)  //设置下一个播放源
 public void onCallNext()  //切换播放设置好的下一个播放源
 public double getDuration();//获取时长（如果有在异步准备好后可获取）
```

## 回调函数

```Java
public interface WlOnCompleteListener  //视频播放完成回调

public interface WlOnErrorListener  //视频播放错误回调

public interface WlOnloadListener   //视频加载回调

public interface WlOnParparedListener  //视频准备就绪可以播放回调

public interface WlOnPauseResumeListener  //视频暂停回调

public interface WlOntimeInfoListener   //播放时间信息回调
```

> Create By Xurent 2020/02/08
