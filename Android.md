```
    Activity           活动（C：逻辑）更小范围的：碎片 Fragment
        Intent - 隐式/显式
        Bundle
        Back Stack (LIFO) --> Task
        mode: 
          standard        (允许重复创建同名活动)
          singleTop       (当栈顶层不是该活动时，才会新创建一个)
          singleTask      (当前栈中存在活动则把上方所有其它活动出栈置顶当前活动，不存在则创建)
          singleInstance  (使用多个不同的栈来处理活动)
        通过 AndroidManifest.xml 配置各活动属性
```

![lifecycle](https://developer.android.com/guide/components/images/activity_lifecycle.png)

```
    Layout             布局（V：视图）
        LinearLayout, RelativeLayout, FrameLayout, PercentXX
        <Button 
          android:id="@+id/button_1" 
          android:layout_width="match_parent" 
          android:layout_height="wrap_content" 
          android:text="Button 1" 
        />
    Widget             控件 (逻辑+视图组合)
        ViewGroup --> View
```

```
    ListView
    public class XxxAdapter extends ArrayAdapter<Xxx> {
    	public XxxAdapter(Context context, int textViewResourceId, List<Xxx> objects){ 
    		super(context, textViewResourceId, objects);
    	}
    
    	@Override
        public View getView(int position, View convertView, ViewGroup parent) {
            
        }
    }
    
    RecyclerView 新增横向和瀑布流布局
    public class xxxAdapter extends RecyclerView.Adapter<xxxAdapter.ViewHolder> {
    	static class ViewHolder extends RecyclerView.ViewHolder{
    		public ViewHolder(View view){
    			super(view)
    		}
    	}
    
    	public xxxAdapter(List<xxx> xxxList){ 
    
    	}
    }
    
    Webview 控件
```

```
    nine-patch 点9
```

```
    Content Provider   内容提供者
        跨程序共享数据(比如读取系统联系人)
            ContentResolver 
                content://io.llo.xxx.provider/table1
                或访问拍照或截屏保存到 /data 目录下的数据
        权限管理：
            危险权限(组) + 普通权限 + 动态检查与申请
```

```
    Broadcast Receiver 广播接收器
        APP内部监听与通知(Notification)，或手机系统自身广播(已开机，网络状态）
        分标准广播与有序广播（链式处理）
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
        
        class MyThread extends Thread{
        	@Override
        	public void run(){ 
        		// logic code
        	}
        }
        new MyThread().start();  // will run in other thread
        
        method2:
        
        class MyThread implements Runnable{ 
        	@Override
        	public void run(){ 
        		// logic code
        	}
        }
        MyThread myThread = new MyThread();
        new Thread(myThread).start();
        
        method3:
        
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
```

```
    Service：并不默认在子线程运行。能够关闭自己。IntentService
        public class MyService extends Service{
        	public MyService(){ 
        
        	}
        
        	@Override
        	public void onCreate(){ 
        		super.onCreate();
        	}
        
        	@Override
        	public int onStartCommand(Intent intent, int flags, int startId){ 
        		return super.onStartCommand(intent, flags, startId);
        	}
        
        	@Override
        	public void onDestory(){ 
        		super.onDestory();
        	}
        
        	@Override
        	public IBinder onBind(Intent intent){ 
        		// ...
        	}
        }
        
        Intent startIntent = new Intent(this, MyService.class);  // this is some activity
        startService(startIntent);
        
        Intent stopIntent = new Intent(this, MyService.class);
        stopService(stopIntent);
```

```
    Theme:
    
```

![ThemeColors](https://developer.android.com/training/material/images/ThemeColors.png)

```
Global:

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
