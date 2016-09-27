<div class="text" style=" text-align:center;"><h1>BroadCast</h1></div>

<h3>1.1 两种广播类型：</h3>

![](http://www.runoob.com/wp-content/uploads/2015/08/72916726.jpg)

<h3>1.2 注册广播：</h3>

动态注册：

![](http://www.runoob.com/wp-content/uploads/2015/08/17322218.jpg)

```
@Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);
       //核心部分代码：
       myReceiver = new BroadcastReceiver();
       IntentFilter itFilter = new IntentFilter();
       itFilter.addAction("android.net.conn.CONNECTIVITY_CHANGE");
       registerReceiver(myReceiver, itFilter);
   }
```

静态注册：

![](http://www.runoob.com/wp-content/uploads/2015/08/93737904.jpg)

```
<receiver android:name=".BroadcastReceiver">
    <intent-filter>
        <action android:name = "android.intent.cation.BOOT_COMPLETED">
    </intent-filter>
</receiver>

<!-- 权限 -->
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED"/>
```

<h3>1.2 发送广播：</h3>

![](http://www.runoob.com/wp-content/uploads/2015/08/47229905.jpg)

`
sendBroadcast(new Intent("com.example.broadcasttest.MY_BROADCAST"));
`

<h3>1.2 注销广播：</h3>

`
unregisterReceiver(myReceiver);
`
