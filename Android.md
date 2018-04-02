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
```

```
    nine-patch 点9
```

```
    Service            服务
```

```
    Content Provider   内容提供者
```

```
    Broadcast Receiver 广播接收器
    APP内部监听与通知，或手机系统广播
```
