```
    Activity: 活动（C逻辑）更小范围的：碎片[Fragment]
        Pass Data: Intent[隐式/显式], Bundle
        Back Stack (LIFO): called Task
        Activity mode: 
          standard        (允许重复创建同名活动)
          singleTop       (当栈顶层不是该活动时，才会新创建一个)
          singleTask      (当前栈中存在活动则把上方所有其它活动出栈置顶当前活动，不存在则创建)
          singleInstance  (使用多个不同的栈来处理活动)
        通过 AndroidManifest.xml 配置各活动属性
```

![lifecycle](https://developer.android.com/guide/components/images/activity_lifecycle.png)

```
    Layout: 布局（V视图）
        Layout mode:
	  LinearLayout
	  RelativeLayout
	  FrameLayout
	  PercentXX
    Widget: 控件 (逻辑+视图组合)
        ViewGroup 包含 View
	ListView, RecyclerView[横向和瀑布流布局], Webview
    Attr, Style, Theme
        values/attrs.xml <declare-styleable> 自定义属性 / layout_width 内置属性
	style 由部分 attr 值构成, obtainStyledAttributes 获取当前 style 下相应的属性值, 一个 view 使用一个 style
	theme 也使用 <style> 标签, 定义在系统级, 属下 view 都能使用
```

```
    Content Provider: 内容提供者
        跨程序共享数据(比如读取系统联系人)
            ContentResolver 
                1.content://io.llo.xxx.provider/table1
                2.访问拍照或截屏保存到 /data 目录下的数据
        权限管理：
            危险权限(组) + 普通权限 + 动态检查与申请
```

```
    Broadcast Receiver 广播接收器
        APP内部监听与通知(Notification)，或手机系统自身广播(已开机，网络状态）
        分标准广播与有序广播（链式处理广播数据）
```

```
    Storage 持久化
        文件存储
        SharedPreferences (KV store)
        SQLite (use adb check file)
        LitePal (ORM)
```

```
    安卓多线程
    
        method1:
        ====================
        class MyThread extends Thread{
        	@Override
        	public void run(){ 
        		// logic code
        	}
        }
        new MyThread().start();  // will run in other thread
        
        method2:
        ====================
        class MyThread implements Runnable{ 
        	@Override
        	public void run(){ 
        		// logic code
        	}
        }
        MyThread myThread = new MyThread();
        new Thread(myThread).start();
        
        method3:
        ====================
        new Thread(new Runnable(){
        	@Override
        	public void run(){ 
        		// logic code
        	}
        }).start()
	
        主线程更新UI (handlerMessage) --- 子线程完成耗时任务通知主线程 (handlerSendMessage add to MessageQueue)
        Looper dispatch to handlerMessage
    
    AsyncTask：启动 new Xxx().execute();
      doInBackground()   --- 耗时任务
      onProgressUpdate() --- UI操作
      onPostExecute()    --- 任务收尾工作
	  
    Service：并不默认在子线程运行。能够关闭自己。可选方案: IntentService	  
```

![ThemeColors](https://developer.android.com/training/material/images/ThemeColors.png)

```
    Global: 全局操作

    public class MyApplication extends Application{
    	
      private static Context context;
    
      @Override
      public void onCreate(){ 
        context = getApplicationContext();
      }
    
      public static Context getContext(){
        return context;
      }
    }

    MyApplication 需要注册为默认 application 类
```

```
    Debug:
      断点
      Attach debugger to Android process 随时发起调试
```

```
    定时任务：
      Timer
      Alarm：set/setExact/setAndAllowWhileIdle/setExactAnd...
```

```
    Release:
      1.生成keystore
      2.生成APK
```
