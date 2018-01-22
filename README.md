# ZWTMusicPlayer
![image](https://github.com/liunianhuaguoyanxi/ZWTMusicPlayer/blob/master/Pic/playOnTheBackground.PNG)
![image](https://github.com/liunianhuaguoyanxi/ZWTMusicPlayer/blob/master/Pic/playTheMusie.PNG)
## ESTMusicPlayer 是基于 DOUAudioStreamer 开发的一款优雅简洁的音乐播放器.

## ZWTMusicPlayer 是基于ESTMusicPlayer的基础上的重构，它移除了ESTMusicPlayer中老旧的远程控制事件的实现方式：

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

      在App启动后开启远程控制事件, 接收来自锁屏界面和上拉菜单的控制
    
    
      [application beginReceivingRemoteControlEvents];
    
      return YES;
    
    }


    - (void)applicationWillTerminate:(UIApplication *)application
    
    {
    
        在App要终止前结束接收远程控制事件, 也可以在需要终止时调用该方法终止
    
        [application endReceivingRemoteControlEvents];
    
     }

    在具体的控制器或其它类中捕获处理远程控制事件

    - (void)remoteControlReceivedWithEvent:(UIEvent *)event{
  
      根据事件的子类型(subtype) 来判断具体的事件类型, 并做出处理
  
        switch (event.subtype)
        {
        
        case UIEventSubtypeRemoteControlPlay:
        
        case UIEventSubtypeRemoteControlPause: {
        
            执行播放或暂停的相关操作 (锁屏界面和上拉快捷功能菜单处的播放按钮)
            
            break;
        }
        case UIEventSubtypeRemoteControlPreviousTrack: {
        
            执行上一曲的相关操作 (锁屏界面和上拉快捷功能菜单处的上一曲按钮)
            
            break;
        }
        case UIEventSubtypeRemoteControlNextTrack: {
        
            执行下一曲的相关操作 (锁屏界面和上拉快捷功能菜单处的下一曲按钮)
            
            break;
        }
        case UIEventSubtypeRemoteControlTogglePlayPause: {
        
            进行播放/暂停的相关操作 (耳机的播放/暂停按钮)
            
            break;
        }
        default:
        
            break;}
            
        }


### 因为iOS7.1后，MPRemoteCommandCenter类已经提供了处理远程控制事件的对象, 包括由外部附件和系统传输控制发送的远程控制事件. 不需要自己创建该类的实例. 
### 所以采取MPRemoteCommandCenter的共享对象来注册远程控制事件

### 具体内容（详细参见源码）：
#### 1.重构了播放的架构，使用MPRemoteCommandCenter的共享对象来注册远程控制事件
#### 2.修复某些闪退bug，支持后台播放控制。
#### 3.修复了有时前台音乐播放切歌时出现计时不准。
#### 4.支持了后台播放音乐时，可控制音乐进度。
#### 5.修正了后台播放音乐时，进度条与前台播放不准的问题。

### 若能给大家带来帮助，记得star🙂
