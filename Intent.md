<div class="text" style=" text-align:center;"><h1>Intent</h1></div>
<h3>1. 显示Intent和隐式Intent的区别</h3>
<blockquote>
<ul>
<li><strong>显式Intent：</strong>通过组件名指定启动的目标组件,比如startActivity(new Intent(A.this,B.class)); 每次启动的组件只有一个
<li><strong>隐式显式Intent:</strong>不指定组件名,而指定Intent的Action,Data,或Category,当我们启动组件时, 会去匹配AndroidManifest.xml相关组件的Intent-filter,逐一匹配出满足属性的组件,当不止一个满足时, 会弹出一个让我们选择启动哪个的对话框。
</blockquote>

<h3>2. Intent的七个属性</h3>
一、ComponentName（组件名称）<br><br>

![](http://www.runoob.com/wp-content/uploads/2015/08/93994466.jpg)
<br><br>
二、Action（动作）<br><br>

![](http://www.runoob.com/wp-content/uploads/2015/08/10976710.jpg)
<br><br>
三、Category(类别)<br><br>

![](http://www.runoob.com/wp-content/uploads/2015/08/97975471.jpg)
<br><br>
四、Data(数据)，Type(MIME类型)<br><br>

![](http://www.runoob.com/wp-content/uploads/2015/08/13299674.jpg)
<br><br>
五、Extra(额外)<br><br>

![](http://www.runoob.com/wp-content/uploads/2015/08/19949418.jpg)
<br><br>
六、Flags（标记）<br><br>

![](http://www.runoob.com/wp-content/uploads/2015/08/65852896.jpg)

<h3>3. 显示Intent的使用例子</h3>

<font color="ff0000">示例1：</font>

```
Intent it = new Intent();
it.setAction(Intent.ACTION_MAIN);
it.addCategory(Intent.CATEGORY_HOME);
startActivity(it);
```

<font color="ff0000">示例2：</font>

```
Intent it = new Intent();
it.setAction(Intent.ACTION_VIEW);
it.setData(Uri.parse("http://www.baidu.com"));
startActivity(it);
```

<font color="ff0000">示例3：</font>

```
Intent it = new Intent(ActivityA,ActivityB.class);
ActivityA.startIntent(it);
```

<h3>3. 隐式Intent</h3>
<h4>3.1 隐式Intent解释</h4>
通过设置Intent的属性，然后再根据属性过滤，找到对应的一个或者多个Activity（应用）。<br>

<font color="ff0000">如图：</font><br>

![](http://www.runoob.com/wp-content/uploads/2015/08/96004503.jpg)

<h4>3.2 自定义隐式Intent</h4>
Step1:<bolokquote><ul><em>代码示例：</em>使用自定义的Action与category来激活另一个Activity<br>
<em>核心代码：</em> 建立第二个Activity的布局,与对应的Activity,在第一个Activity的按钮点击事件中添加一下代码:</ul></blockquote>


```
Intent it = new Intent();
it.setAction("my_action");
it.addCategory("my_category");
startActivity(it);
```

<br><br>
Step2:<bolokquote><ul><em>最后在第二个Activity的Intent中添加以下代码:</em></ul></blockquote>

```
<activity android:name=".SecondActivity"
        android:label="第二个Activity">
    <intent-filter>
        <action android:name="my_action"/>
        <category android:name="my_category"/>
        <category android:name="android.intent.category.DEFAULT"/>
    </intent-filter>           
</activity>
```

<br><br>
Step3:<bolokquote><ul><em>添加默认的category:</em></ul></blockquote>

```
<category android:name="android.intent.category.DEFAULT"/>
```

<h3>3. 常用的系统Intent合集</h3>

```
//===============================================================
//1.拨打电话
// 给移动客服10086拨打电话
Uri uri = Uri.parse("tel:10086");
Intent intent = new Intent(Intent.ACTION_DIAL, uri);
startActivity(intent);

//===============================================================

//2.发送短信
// 给10086发送内容为“Hello”的短信
Uri uri = Uri.parse("smsto:10086");
Intent intent = new Intent(Intent.ACTION_SENDTO, uri);
intent.putExtra("sms_body", "Hello");
startActivity(intent);

//3.发送彩信（相当于发送带附件的短信）
Intent intent = new Intent(Intent.ACTION_SEND);
intent.putExtra("sms_body", "Hello");
Uri uri = Uri.parse("content://media/external/images/media/23");
intent.putExtra(Intent.EXTRA_STREAM, uri);
intent.setType("image/png");
startActivity(intent);

//===============================================================

//4.打开浏览器:
// 打开百度主页
Uri uri = Uri.parse("http://www.baidu.com");
Intent intent  = new Intent(Intent.ACTION_VIEW, uri);
startActivity(intent);

//===============================================================

//5.发送电子邮件:(阉割了Google服务的没戏!!!!)
// 给someone@domain.com发邮件
Uri uri = Uri.parse("mailto:someone@domain.com");
Intent intent = new Intent(Intent.ACTION_SENDTO, uri);
startActivity(intent);
// 给someone@domain.com发邮件发送内容为“Hello”的邮件
Intent intent = new Intent(Intent.ACTION_SEND);
intent.putExtra(Intent.EXTRA_EMAIL, "someone@domain.com");
intent.putExtra(Intent.EXTRA_SUBJECT, "Subject");
intent.putExtra(Intent.EXTRA_TEXT, "Hello");
intent.setType("text/plain");
startActivity(intent);
// 给多人发邮件
Intent intent=new Intent(Intent.ACTION_SEND);
String[] tos = {"1@abc.com", "2@abc.com"}; // 收件人
String[] ccs = {"3@abc.com", "4@abc.com"}; // 抄送
String[] bccs = {"5@abc.com", "6@abc.com"}; // 密送
intent.putExtra(Intent.EXTRA_EMAIL, tos);
intent.putExtra(Intent.EXTRA_CC, ccs);
intent.putExtra(Intent.EXTRA_BCC, bccs);
intent.putExtra(Intent.EXTRA_SUBJECT, "Subject");
intent.putExtra(Intent.EXTRA_TEXT, "Hello");
intent.setType("message/rfc822");
startActivity(intent);

//===============================================================

//6.显示地图:
// 打开Google地图中国北京位置（北纬39.9，东经116.3）
Uri uri = Uri.parse("geo:39.9,116.3");
Intent intent = new Intent(Intent.ACTION_VIEW, uri);
startActivity(intent);

//===============================================================

//7.路径规划
// 路径规划：从北京某地（北纬39.9，东经116.3）到上海某地（北纬31.2，东经121.4）
Uri uri = Uri.parse("http://maps.google.com/maps?f=d&saddr=39.9 116.3&daddr=31.2 121.4");
Intent intent = new Intent(Intent.ACTION_VIEW, uri);
startActivity(intent);

//===============================================================

//8.多媒体播放:
Intent intent = new Intent(Intent.ACTION_VIEW);
Uri uri = Uri.parse("file:///sdcard/foo.mp3");
intent.setDataAndType(uri, "audio/mp3");
startActivity(intent);

//获取SD卡下所有音频文件,然后播放第一首=-=
Uri uri = Uri.withAppendedPath(MediaStore.Audio.Media.INTERNAL_CONTENT_URI, "1");
Intent intent = new Intent(Intent.ACTION_VIEW, uri);
startActivity(intent);

//===============================================================

//9.打开摄像头拍照:
// 打开拍照程序
Intent intent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
startActivityForResult(intent, 0);
// 取出照片数据
Bundle extras = intent.getExtras();
Bitmap bitmap = (Bitmap) extras.get("data");

//另一种:
//调用系统相机应用程序，并存储拍下来的照片
Intent intent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
time = Calendar.getInstance().getTimeInMillis();
intent.putExtra(MediaStore.EXTRA_OUTPUT, Uri.fromFile(new File(Environment
.getExternalStorageDirectory().getAbsolutePath()+"/tucue", time + ".jpg")));
startActivityForResult(intent, ACTIVITY_GET_CAMERA_IMAGE);

//===============================================================

//10.获取并剪切图片
// 获取并剪切图片
Intent intent = new Intent(Intent.ACTION_GET_CONTENT);
intent.setType("image/*");
intent.putExtra("crop", "true"); // 开启剪切
intent.putExtra("aspectX", 1); // 剪切的宽高比为1：2
intent.putExtra("aspectY", 2);
intent.putExtra("outputX", 20); // 保存图片的宽和高
intent.putExtra("outputY", 40);
intent.putExtra("output", Uri.fromFile(new File("/mnt/sdcard/temp"))); // 保存路径
intent.putExtra("outputFormat", "JPEG");// 返回格式
startActivityForResult(intent, 0);
// 剪切特定图片
Intent intent = new Intent("com.android.camera.action.CROP");
intent.setClassName("com.android.camera", "com.android.camera.CropImage");
intent.setData(Uri.fromFile(new File("/mnt/sdcard/temp")));
intent.putExtra("outputX", 1); // 剪切的宽高比为1：2
intent.putExtra("outputY", 2);
intent.putExtra("aspectX", 20); // 保存图片的宽和高
intent.putExtra("aspectY", 40);
intent.putExtra("scale", true);
intent.putExtra("noFaceDetection", true);
intent.putExtra("output", Uri.parse("file:///mnt/sdcard/temp"));
startActivityForResult(intent, 0);

//===============================================================

//11.打开Google Market
// 打开Google Market直接进入该程序的详细页面
Uri uri = Uri.parse("market://details?id=" + "com.demo.app");
Intent intent = new Intent(Intent.ACTION_VIEW, uri);
startActivity(intent);

//===============================================================

//12.进入手机设置界面:
// 进入无线网络设置界面（其它可以举一反三）  
Intent intent = new Intent(android.provider.Settings.ACTION_WIRELESS_SETTINGS);  
startActivityForResult(intent, 0);

//===============================================================

//13.安装apk:
Uri installUri = Uri.fromParts("package", "xxx", null);   
returnIt = new Intent(Intent.ACTION_PACKAGE_ADDED, installUri);

//===============================================================

//14.卸载apk:
Uri uri = Uri.fromParts("package", strPackageName, null);      
Intent it = new Intent(Intent.ACTION_DELETE, uri);      
startActivity(it);

//===============================================================

//15.发送附件:
Intent it = new Intent(Intent.ACTION_SEND);      
it.putExtra(Intent.EXTRA_SUBJECT, "The email subject text");      
it.putExtra(Intent.EXTRA_STREAM, "file:///sdcard/eoe.mp3");      
sendIntent.setType("audio/mp3");      
startActivity(Intent.createChooser(it, "Choose Email Client"));

//===============================================================

//16.进入联系人页面:
Intent intent = new Intent();
intent.setAction(Intent.ACTION_VIEW);
intent.setData(People.CONTENT_URI);
startActivity(intent);

//===============================================================


//17.查看指定联系人:
Uri personUri = ContentUris.withAppendedId(People.CONTENT_URI, info.id);//info.id联系人ID
Intent intent = new Intent();
intent.setAction(Intent.ACTION_VIEW);
intent.setData(personUri);
startActivity(intent);

//===============================================================

//18.调用系统编辑添加联系人（高版本SDK有效）：
Intent it = newIntent(Intent.ACTION_INSERT_OR_EDIT);    
it.setType("vnd.android.cursor.item/contact");    
//it.setType(Contacts.CONTENT_ITEM_TYPE);    
it.putExtra("name","myName");    
it.putExtra(android.provider.Contacts.Intents.Insert.COMPANY, "organization");    
it.putExtra(android.provider.Contacts.Intents.Insert.EMAIL,"email");    
it.putExtra(android.provider.Contacts.Intents.Insert.PHONE,"homePhone");    
it.putExtra(android.provider.Contacts.Intents.Insert.SECONDARY_PHONE,"mobilePhone");    
it.putExtra( android.provider.Contacts.Intents.Insert.TERTIARY_PHONE,"workPhone");    
it.putExtra(android.provider.Contacts.Intents.Insert.JOB_TITLE,"title");    
startActivity(it);

//===============================================================

//19.调用系统编辑添加联系人（全有效）：
Intent intent = newIntent(Intent.ACTION_INSERT_OR_EDIT);    
intent.setType(People.CONTENT_ITEM_TYPE);    
intent.putExtra(Contacts.Intents.Insert.NAME, "My Name");    
intent.putExtra(Contacts.Intents.Insert.PHONE, "+1234567890");    
intent.putExtra(Contacts.Intents.Insert.PHONE_TYPE,Contacts.PhonesColumns.TYPE_MOBILE);    
intent.putExtra(Contacts.Intents.Insert.EMAIL, "com@com.com");    
intent.putExtra(Contacts.Intents.Insert.EMAIL_TYPE, Contacts.ContactMethodsColumns.TYPE_WORK);    
startActivity(intent);

//===============================================================

//20.打开另一程序
Intent i = new Intent();     
ComponentName cn = new ComponentName("com.example.jay.test",     
"com.example.jay.test.MainActivity");     
i.setComponent(cn);     
i.setAction("android.intent.action.MAIN");     
startActivityForResult(i, RESULT_OK);

//===============================================================

//21.打开录音机
Intent mi = new Intent(Media.RECORD_SOUND_ACTION);     
startActivity(mi);

//===============================================================

//22.从google搜索内容
Intent intent = new Intent();     
intent.setAction(Intent.ACTION_WEB_SEARCH);     
intent.putExtra(SearchManager.QUERY,"searchString")     
startActivity(intent);

//===============================================================
```

<h3>4. Intent复杂数据的传递</h3>
<h4>4.1 Intent传递简单数据</h4>

![](http://www.runoob.com/wp-content/uploads/2015/08/71858311.jpg)

<h4>4.2 Intent传递数组</h4>
写入数组

```
bd.putStringArray("StringArray", new String[]{"呵呵","哈哈"});
//可把StringArray换成其他数据类型,比如int,float等等...
```

读取数组

```
String[] str = bd.getStringArray("StringArray")
```

<h4>4.2 Intent传递集合</h4>
<li>List<基本数据或String>

写入数据

```
intent.putStringArrayListExtra(name, value)
intent.putIntegerArrayListExtra(name, value)
```

读取集合

```
intent.getStringArrayListExtra(name)
intent.getIntegerArrayListExtra(name)
```

<li>List<Object>(这里Object需实现serializable接口)

将list强转成Serializable类型,然后传入(可用Bundle做媒介),采用序列化的模式。

写入集合

```
putExtras(key, (Serializable)list)
```

读取集合

```
(List<Object>) getIntent().getSerializable(key)
```

<li>Map<String, Object>,或更复杂的

解决方法是：外层套个List

```
//传递复杂些的参数
Map<String, Object> map1 = new HashMap<String, Object>();  
map1.put("key1", "value1");  
map1.put("key2", "value2");  
List<Map<String, Object>> list = new ArrayList<Map<String, Object>>();  
list.add(map1);  

Intent intent = new Intent();  
intent.setClass(MainActivity.this,ComplexActivity.class);  
Bundle bundle = new Bundle();  

//须定义一个list用于在budnle中传递需要传递的ArrayList<Object>,这个是必须要的  
ArrayList bundlelist = new ArrayList();   
bundlelist.add(list);   
bundle.putParcelableArrayList("list",bundlelist);  
intent.putExtras(bundle);                
startActivity(intent);
```

<h4>4.4 Intent传递对象</h4>
传递对象的方式有两种：将对象转换为<em>Json</em>字符串或者通过<em>Serializable,Parcelable</em>序列化

<li>将对象转换成Json字符串

<font color="ff0000">示例：</font>

Model

```
public class Author{
    private int id;
    private String name;
    //...
}

public class Author{
    private int id;
    private String name;
    //...
}
```

写入数据

```
Book book=new Book();
book.setTitle("Java编程思想");
Author author=new Author();
author.setId(1);
author.setName("Bruce Eckel");
book.setAuthor(author);
Intent intent=new Intent(this,SecondActivity.class);
intent.putExtra("book",new Gson().toJson(book));
startActivity(intent);
```

读取数据

```
String bookJson=getIntent().getStringExtra("book");
Book book=new Gson().fromJson(bookJson,Book.class);
Log.d(TAG,"book title->"+book.getTitle());
Log.d(TAG,"book author name->"+book.getAuthor().getName());
```

<li>使用Serialization，Parcelable序列化对象

Serializable实现流程：

<ol><li>业务Bean实现：Serializable接口,写上getter和setter方法
<li>Intent通过调用putExtra(String name, Serializable value)传入对象实例 当然对象有多个的话多个的话,我们也可以先Bundle.putSerializable(x,x);
<li>新Activity调用getSerializableExtra()方法获得对象实例: eg:Product pd = (Product) getIntent().getSerializableExtra("Product");
<li>调用对象get方法获得相应参数</ol>

Parcelable实现流程：

<ol><li>业务Bean继承Parcelable接口,重写writeToParcel方法,将你的对象序列化为一个Parcel对象;
<li>重写describeContents方法，内容接口描述，默认返回0就可以
<li>实例化静态内部对象CREATOR实现接口Parcelable.Creator
<li>同样式通过Intent的putExtra()方法传入对象实例,当然多个对象的话,我们可以先 放到Bundle里Bundle.putParcelable(x,x),再Intent.putExtras()即可</ol>
