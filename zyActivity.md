<div class="text" style=" text-align:center;"><h1>Activity</h1></div>

<h2>Activity的概念</h2>

Activity是一个应用程序的组件，他在屏幕上提供了一个区域，允许用户在上面做一些交互性的操作。
Activity可以理解成一个绘制用户界面的窗口，
而这个窗口可以填满整个屏幕，也可能比屏幕小或者浮动在其他窗口的上方！

<h3>1.1 Activity的生命周期</h3>

![](http://www.runoob.com/wp-content/uploads/2015/08/18364230.jpg)

<h3>1.2 Activity的创建流程</h3>

![](http://www.runoob.com/wp-content/uploads/2015/08/48768883.jpg)

注意：

```
public void onSaveInstanceState(Bundle outState, PersistableBundle outPersistentState)
public void onRestoreInstanceState(Bundle savedInstanceState, PersistableBundle persistentState)
```

<blockquote><ul>
<li>点击home键回到主页或长按后选择运行其他程序
<li>按下电源键关闭屏幕
<li>启动新的Activity
<li>横竖屏切换时，肯定会执行，因为横竖屏切换的时候会先销毁Act，然后再重新创建 重要原则：
当系统"未经你许可"时销毁了你的activity，则onSaveInstanceState会被系统调用， 这是系统的责任，
因为它必须要提供一个机会让你保存你的数据（你可以保存也可以不保存）。
</ul></blockquote>

<h3>1.3 Activity的启动</h3>

1、显式启动：通过包名来启动，写法如下：

<li>常见的ActivityA启动ActivityB

```
startActivity(new Intent(ActivityA.this,ActivityB.class));
```

<li>通过Intent的ComponentName:

```
ComponentName cn = new ComponentName("当前Act的全限定类名","启动Act的全限定类名") ;
Intent intent = new Intent() ;
intent.setComponent(cn) ;
startActivity(intent) ;
```

<li>初始化Intent时指定包名

```
Intent intent = new Intent("android.intent.action.MAIN");
intent.setClassName("当前Act的全限定类名","启动Act的全限定类名");
startActivity(intent);
```

注意：startActivity（）方法最后调用的是startActivityForResult()的方法。

2、隐式启动：写法如下

```
Intent intent = new Intent();
intent.setAction("my_action");
intent.addCategory("my_category");
startActivity(intent);
```

3、直接通过包名启动apk:

```
Intent intent=getPackageManager().getLaunchIntentForPackage
("apk第一个启动Activity的全限定类名")
if(intent != null){
  startActivity(intent);
}
```

<h3>1.4 Activity的数据传递</h3>

通过Intent传递数据（略）。

<h3>1.5 知晓当前是哪一个Activity</h3>

让所有的Activity继承一个自定义的BaseActivity类，在OnCreate（）方法中添加下述语句即可：

```
getClass().getSimpleName();
```

<h3>1.6 关闭所有的Activity</h3>

<font color="ff0000">流程</font>

![](http://www.runoob.com/wp-content/uploads/2015/08/59443692.jpg)

<font color="ff0000">代码</font>

```
public class ActivityCollector {
    public static LinkedList<Activity> activities = new LinkedList<Activity>();
    public static void addActivity(Activity activity)
    {
        activities.add(activity);
    }
    public static void removeActivity(Activity activity)
    {
        activities.remove(activity);
    }
    public static void finishAll()
    {
        for(Activity activity:activities)
        {
            if(!activity.isFinishing())
            {
                activity.finish();
            }
        }
    }
}
```

<Strong>注意：</strong>完全退出App的方法

<font color="ff0000">代码</font>

```
/**
 * 退出应用程序
 */
public void AppExit(Context context) {
    try {
        ActivityCollector.finishAll();
        ActivityManager activityMgr = (ActivityManager) context
                .getSystemService(Context.ACTIVITY_SERVICE);
        activityMgr.killBackgroundProcesses(context.getPackageName());
        System.exit(0);
    } catch (Exception ignored) {}
}
```

<h3>1.7 Activity的进出动画</h3>

![](http://www.runoob.com/wp-content/uploads/2015/08/16878455.jpg)

<h3>1.8 Activity设置全屏</h3>

<li>代码隐藏ActionBar

在Activity的onCreate方法中调用getActionBar.hide()。

<li>通过requestWindowFeature设置

requestWindowFeature(Window.FEATURE_NO_TITLE); 该代码需要在setContentView ()之前调用，不然会报错！！！

<li>通过AndroidManifest.xml设置theme

在需要全屏的Activity的标签内设置 theme = @android:style/Theme.NoTitleBar.FullScreen

<h2>2. Activity的进阶</h2>

<h3>2.1 Activity、Window与View的关系</h3>

![](http://www.runoob.com/wp-content/uploads/2015/08/93497523.jpg)

<font color="ff0000">流程解析：</font>

Activity调用startActivity后最后会调用attach方法，然后在PolicyManager实现一个Ipolicy接口，
 接着实现一个Policy对象，接着调用makenewwindow(Context)方法，该方法会返回一个PhoneWindow对象，
  而PhoneWindow 是Window的子类，在这个PhoneWindow中有一个DecorView的内部类，是所有应用窗口的根View，
   即View的老大， 直接控制Activity是否显示(引用老司机原话…)，好吧，接着里面有一个LinearLayout，
   里面又有两个FrameLayout他们分别拿来装ActionBar和CustomView，
、而我们setContentView()加载的布局就放到这个CustomView中！

<h3>2.2 Activity、Task与Back Stack的关系</h3>

我们的APP一般都是由多个Activity构成的，而在Android中给我们提供了一个Task(任务)的概念，
 就是将多个相关的Activity收集起来，然后进行Activity的跳转与返回！

 <font color="ff0000">流程图：</font>

![ ](http://www.runoob.com/wp-content/uploads/2015/08/93537362.jpg)

<h3>2.3 Activity的Task管理</h3>

代码中通过传递特殊标识的Intent给startActivity( )就可以轻松的实现 对Actvitiy的管理了。

<strong>Activity中可以使用的属性如下</strong>

<blockquote><ul>
<li>taskAffinity
<li>launchMode
<li>allowTaskReparenting
<li>clearTaskOnLaunch
<li>alwaysRetainTaskState
<li>finshOnTaskLaunch
</ul></blockquote>

<strong>Intent的主要标志</strong>

<blockquote><ul>
<li>FLAG_ACTIVITY_NEW_TASK
<li>FLAG_ACTIVITY_CLEAR_TOP
<li>FLAG_ACTIVITY_SINGLE_TOP
</ul></blockquote>

<h3>2.4 Activity的四种启动模式</h3>

<blockquote><ul>
<li>standard
<li>singleTop
<li>singleTask
<li>singleInstance
</ul></blockquote>

<strong>一、standard模式</strong>

标准启动模式，也是activity的默认启动模式。在这种模式下启动的activity可以被多次实例化，
 即在同一个任务中可以存在多个activity的实例，每个实例都会处理一个Intent对象。
 如果Activity A的启动模式为standard，并且A已经启动，在A中再次启动Activity A，
  即调用startActivity（new Intent（this，A.class）），
 会在A的上面再次启动一个A的实例，即当前的桟中的状态为A–>A。

 <strong>二、singleTop模式</strong>

 如果一个以singleTop模式启动的Activity的实例已经存在于任务栈的栈顶，
 那么再启动这个Activity时，不会创建新的实例，而是重用位于栈顶的那个实例，
 并且会调用该实例的onNewIntent()方法将Intent对象传递到这个实例中。

 如果以singleTop模式启动的activity的一个实例 已经存在与任务栈中，
  但是不在栈顶，那么它的行为和standard模式相同，也会创建多个实例。

<strong>三、singleTask模式</strong>

只允许在系统中有一个Activity实例。如果系统中已经有了一个实例， 持有这个实例的任务将移动到顶部，
同时intent将被通过onNewIntent()发送。
 如果没有，则会创建一个新的Activity并置放在合适的任务中。

 <strong>四、singleInstance模式</strong>

 保证系统无论从哪个Task启动Activity都只会创建一个Activity实例,并将它加入新的Task栈顶
 也就是说被该实例启动的其他activity会自动运行于另一个Task中。 当再次启动该activity的实例时，
  会重用已存在的任务和实例。并且会调用这个实例 的onNewIntent()方法，
  将Intent实例传递到该实例中。和singleTask相同， 同一时刻在系统中只会存在一个这样的Activity实例。
