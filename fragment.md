<h2>Fragmrnt</h2>
<h2>1. 基本概念</h2><br>
   Fragmnet是Android3.0后引入的一个新的API，我们可以把他看成一个小型的Activity，又称为Activity片段！
   另外Fragment并不能单独的使用，它需要嵌套在Activity中使用,尽管他拥有这自己的生命周期，还是会受到宿主
   Activity生命周期的影响，比如Activity别destory销毁了，他也会跟着销毁！<br>
<br>
<h3>1.1 生命周期<br></h3>
<br>
![](http://www.runoob.com/wp-content/uploads/2015/08/31722863.jpg)<br>
<br>
<ul><li>Fragment的生命周期和Activity有点类似:<br>三种状态:<br>
(1) Resumed:在允许中的Fragment可见<br>
(2) Paused:所在Activity可见,但是得不到焦点<br>
(3) Stoped:
①调用addToBackStack(),Fragment被添加到Bcak栈
②该Activity转向后台,或者该Fragment被替换/删除<br>
ps:停止状态的fragment仍然活着(所有状态和成员信息被系统保持着),然而,它对用户
不再可见,并且如果activity被干掉,他也会被干掉.</li></ul>

<h3>1.2 Fragment的子类</h3>
<blockquote><ul>
<li>对话框:<strong>DialogFragment</strong></li>
<li>列表:<strong>ListFragment</strong></li>
<li>选项设置:<strong>PreferenceFragment</strong></li>
<li>WebView界面:<strong>WebViewFragment</strong></li>
</ul>
</blockquote>
<h2>2. Fragment的基本业务</h2>
<h3>2.1 创建Fragment</h3>
<li>静态加载Fragment</li><br>

```
public class Fragmentone extends Fragment {
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
            Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fragment1, container,false);
        return view;
    }   
}
```
<li>动态加载Fragment</li>
<br>
<font color="ff0000">流程图</font><br><br>

![](http://www.runoob.com/wp-content/uploads/2015/08/29546434.jpg)

<font color="ff0000">关键代码</font><br>

```
public class MainActivity extends Activity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Display dis = getWindowManager().getDefaultDisplay();
        if(dis.getWidth() > dis.getHeight())
        {
            Fragment1 f1 = new Fragment1();
            getFragmentManager().beginTransaction().replace(R.id.LinearLayout1, f1).commit();
        }

        else
        {
            Fragment2 f2 = new Fragment2();
            getFragmentManager().beginTransaction().replace(R.id.LinearLayout1, f2).commit();
        }
    }   
}
```

<h3>2.2 Fragment和Activity的交互</h3>
<h4>2.2.1 获取组件</h4>
<ul><li><strong>Fragment获取Activity中的组件：</strong><font color="ff0000">getActivity().findViewById(R.id.list);</font></li></ul>
<ul><li><strong>Activity获取Fragment中的组件：</strong><font color="ff0000">getFragmentManager.findFragmentByid(R.id.Fragment1);</font></li></ul>

<h4>2.2.1 数据传递</h4>
<ul>
<li><strong>Activity传递数据给Fragment：</strong>
<br>在Activity中创建Bundle数据包,调用Fragment实例的setArguments(bundle) 从而将Bundle数据包传给Fragment,然后Fragment中调用getArguments获得 Bundle对象,然后进行解析就可以了。<br><br>
</li>
<li><strong>Fragment传递数据给Activity：</strong>
<br>在Fragment中定义一个内部回调接口,再让包含该Fragment的Activity实现该回调接口, Fragment就可以通过回调接口传数据了,回调。<br><br>
</li>
</ul>

<h3>2.3 DialogFrament解析</h3>
（Google推荐使用DialogFragment）<br>
<h4>2.3.1 DialogFrament概念：</h4>
<Strong>DialogFrament</strong>是展示Dialog窗口的Fragment。这个fragment包含了一个Dialog对象，它的展示是基于fragment的状态。<br><u>控制dialog（决定要show，hide，dismiss等）应该通过dialogfragment的api而不是dialog的</u>。<br>

<strong>Step1:</strong> 创建DialogFragment<br>
通过override方法<strong>onCreateView(LayoutInflater, ViewGroup, Bundle)</strong>来填充dialog的内容（也可以override方法onCreateDialog(Bundle)来创建一个完全自定义的dialog）。

<font color="ff0000">示例</font><br>

```
public static class MyDialogFragment extends DialogFragment {  
    static MyDialogFragment newInstance() {  
        return new MyDialogFragment();  
    }  

    @Override  
    public View onCreateView(LayoutInflater inflater, ViewGroup container,  
            Bundle savedInstanceState) {  
        View v = inflater.inflate(R.layout.hello_world, container, false);  
        View tv = v.findViewById(R.id.text);  
        ((TextView)tv).setText("This is an instance of MyDialogFragment");  
        return v;  
    }  
}  
```
<strong>Step2:</strong> 显示DialogFragment<br>
<br>
<font color="ff0000">示例</font><br>

```
void showDialog() {  
    // Create the fragment and show it as a dialog.  
    DialogFragment newFragment = MyDialogFragment.newInstance();  
    newFragment.show(getFragmentManager(), "dialog");  
}  
```

<h4>2.3.2 DialogFrament的销毁</h4>
<ul><li>dismiss()</li>
<li>dismissAllowLoseState:允许状态值丢失</li>
</ul>

<h4>2.3.3 DialogFrament的常见报错及问题</h4>
<strong>问题一：</strong><br>

`
Fragmnet(XXFragment) not attached to Activity
`
<br>
出现该异常，是因为Fragment的还没有Attach到Activity时，调用了如getResource()等，需要上下文Content的函数。解决办法是将操作放在<u>onStart()</u>绑定之后，或是添加<u>if（isAdd）</u>的判断,是否绑定。<br>

<br><br>
<strong>问题二：</strong><br><br>
`
java.lang.IllegalStateException: Can not perform this action after onSaveInstanceState
`
<br><br>
出现该异常，一般是指DoalogFragment的状态值在onSaveInstanceState保存失败，如Fragment快速切换的时候。解决办法是：使用<u>commitAllowLoseState（）</u>代替<u>commit（）</u>。<br>

<br>
<strong>问题三：</strong><br><br>

`
Dialogfragment在旋转屏幕或者修改系统设置后，Activity和DialogFragment的重新绘制
`
<br><br>
只要理解了Fragment 和 Activity 生命周期就会知道原因其实很简单：
<tr>
1. 旋转屏幕时，Activity将会被重新创建。<br>
2. Activity“临终”前会在onSaveInstanceState()中保存 DialogFragment的状态(FragmentManagerState);
3. “复活”后的Activity，在onCreate()中会根据savedInstanceState所给予的FragmentManagerState自动重新实例化DialogFragment，并且 show()出 dialog。<br>
<font color="ff0000">流程为：</font><br>

`
旋转屏幕-->-Activity.onSaveInstanceState()-->-Activity.onCreate()-->-DialogFragment.show()--
`
 <br></tr>
解决办法：OnCreate（）中通过FragmentManagerState找到重新实例化的DialogFragment，重新设置其属性。

<br>
<strong>问题四：</strong><br><br>

`
FragmentDialog同时也具有Dialog的属性，所以在显示和销毁Fragment的时候都应该做判断，否则回报状态异常的错误。
`
<br><br>
解决办法：显示的时候，需要判断当前DialogFragment是否已经添加并显示if(fragment.isAdded())。销毁的时候需要判断绑定的Activity的状态，是否存在if(context != null)。使用dismissAllowingStateLoss（）代替dismiss（）。
