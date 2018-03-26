```
    Activity           活动（C：逻辑）
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
    Widget             控件
```

```
    Service            服务
```

```
    Content Provider   内容提供者
```

```
    Broadcast Receiver 广播接收器
```
