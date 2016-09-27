本文主要分为：<br>
一、Activity详解<br>
二、Service详解<br>
三、Broadcast Receiver详解<br>
四、Content Provider详解<br>
外加一个重要组件 intent的详解。<br>
<br>
文章有部分内容来自网络，本文是一个总结性文章。<br>
<br>
<strong><font size="5">一、Activity详解</font></strong><br>
Activty的生命周期的也就是它所在进程的生命周期。<br>
<div align="left"><font size="2"><font color="#333333"><br>
</font></font></div><br>

<img id="aimg_12282" aid="12282" src="http://www.apkbus.com/data/attachment/forum/201112/07/1630011qa0lv8s0lqadr1d.jpg" zoomfile="data/attachment/forum/201112/07/1630011qa0lv8s0lqadr1d.jpg" file="data/attachment/forum/201112/07/1630011qa0lv8s0lqadr1d.jpg" class="zoom" onclick="zoom(this, this.src, 0, 0, 0)" width="572" inpost="1" onmouseover="showMenu({'ctrlid':this.id,'pos':'12'})" initialized="true">

<div class="tip tip_4 aimg_tip" id="aimg_12282_menu" style="position: absolute; z-index: 301; left: 619.5px; top: 785px; display: none;" disautofocus="true" initialized="true">
<div class="xs0">
<p><strong>1.jpg</strong> <em class="xg1">(32.68 KB, 下载次数: 353)</em></p>
<p>
<a href="http://www.apkbus.com/forum.php?mod=attachment&amp;aid=MTIyODJ8ZDE5MjhiZTl8MTQ2MTEyOTUwNHwwfDE4MjA0&amp;nothumb=yes" target="_blank" class="gj_safe_a">下载附件</a>

</p>

<p class="xg1 y">2011-12-7 16:30 上传</p>

</div>
<div class="tip_horn"></div>
</div>

<br>
<br>
一个Activity的启动顺序：<strong><font color="#333333"><font face="&amp;quot;"><font style="font-size:10.5pt"><br>
</font></font></font></strong><br>
<strong><font color="#333333"><font face="&amp;quot;"><font style="font-size:10.5pt">onCreate()——&gt;</font></font></font>onStart()<font color="#333333"><font face="Arial, sans-serif">——&gt;</font></font>onResume()</strong><br>
<br>
当另一个Activity启动时:<br>
<strong><font color="#333333"><font face="宋体"><font style="font-size:10.5pt">第一个</font></font></font><font color="#333333"><font face="&amp;quot;"><font style="font-size:10.5pt">Activity onPause()</font></font></font><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">——&gt;</font></font></font><font style="color:rgb(51, 51, 51)"><font face="宋体"><font style="font-size:10.5pt">第二个</font></font></font><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">Activity&nbsp; &nbsp; </font></font></font><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">onCreate()——&gt;</font></font></font>onStart()<font color="#333333"><font face="Arial, sans-serif">——&gt;</font></font>onResume() </strong><br>
<strong><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">——&gt;</font></font></font><font color="#333333"><font face="宋体"><font style="font-size:10.5pt">第一个</font></font></font><font color="#333333"><font face="&amp;quot;"><font style="font-size:10.5pt">Activity&nbsp; &nbsp;</font></font></font>onStop()</strong><br>
<br>
当返回到第一个Activity时：<br>
<strong><font color="#333333"><font face="宋体"><font style="font-size:10.5pt">第二个</font></font></font><font color="#333333"><font face="&amp;quot;"><font style="font-size:10.5pt">Activity onPause() </font></font></font><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">——&gt; </font></font></font><font style="color:rgb(51, 51, 51)"><font face="宋体"><font style="font-size:10.5pt">第一个</font></font></font><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">Activity</font></font></font><font style="color:rgb(51, 51, 51)"><font face="宋体"><font style="font-size:10.5pt">　</font></font></font><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">onRestart()</font></font></font><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">——&gt;</font></font></font>onStart()<font color="#333333"><font face="Arial, sans-serif">——&gt;</font></font>onResume() </strong><br>
<font color="#333333"><font face="&amp;quot;"><font style="font-size:10.5pt"><strong>——&gt;第二个Activity&nbsp; &nbsp;onStop()</strong></font></font></font><strong><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">——&gt;</font></font></font></strong><strong>onDestroy()</strong><br>
<br>
一个Activity的销毁顺序:<br>
<strong><font color="#333333"><font face="宋体"><font style="font-size:10.5pt">（情况一）</font></font></font><font color="#333333"><font face="&amp;quot;"><font style="font-size:10.5pt">onPause()</font></font></font></strong><strong><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">——&gt;</font></font></font><font face="Calibri, sans-serif"><font style="font-size:10.5pt">&lt;Process Killed&gt;</font></font> </strong><br>
<font color="#333333"><font face="&amp;quot;"><font style="font-size:10.5pt"><strong>（情况二）onPause()</strong></font></font></font><strong><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">——&gt;</font></font></font></strong><strong>onStop()</strong><strong><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">——&gt;</font></font></font></strong><strong><font face="Calibri, sans-serif"><font style="font-size:10.5pt">&lt;Process Killed&gt;</font></font> </strong><br>
<font color="#333333"><font face="&amp;quot;"><font style="font-size:10.5pt"><strong>（情况三）onPause()</strong></font></font></font><strong><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">——&gt;</font></font></font></strong><strong>onStop()</strong><strong><font style="color:rgb(51, 51, 51)"><font face="Arial, sans-serif"><font style="font-size:10.5pt">——&gt;</font></font></font></strong><strong>onDestroy()</strong><br>
<br>
　　每一个活动（ Activity ）都处于某一个状态，对于开发者来说，是无法控制其应用程序处于某一个状态的，这些均由系统来完成。<br>
<br>
　　但是当一个活动的状态发生改变的时候，开发者可以通过调用 onXX() 的方法获取到相关的通知信息。<br>
<br>
　　在实现 Activity 类的时候，通过覆盖（ override ）这些方法即可在你需要处理的时候来调用。<br>
<br>
<br>
<div align="left">&nbsp; &nbsp;&nbsp; &nbsp; <strong>&nbsp;&nbsp;一、 onCreate</strong> ：当活动第一次启动的时候，触发该方法，可以在此时完成活动的初始化工作。 <br>
onCreate 方法有一个参数，该参数可以为空（ null ），也可以是之前调用 onSaveInstanceState （）方法保存的状态信息。 </div><div align="left">&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;<strong>二、&nbsp;&nbsp;onStart</strong> ：该方法的触发表示所属活动将被展现给用户。 </div><div align="left">&nbsp; &nbsp;&nbsp; &nbsp;<strong>&nbsp;&nbsp;三、&nbsp;&nbsp;onResume</strong> ：当一个活动和用户发生交互的时候，触发该方法。 </div><div align="left">&nbsp; &nbsp;&nbsp; &nbsp; <strong> 四、&nbsp;&nbsp;onPause </strong>：当一个正在前台运行的活动因为其他的活动需要前台运行而转入后台运行的时候，触发该方法。这时候需要将活动的状态持久化，比如正在编辑的数据库记录等。 </div><div align="left">&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;<strong>五、&nbsp;&nbsp;onStop</strong> ：当一个活动不再需要展示给用户的时候，触发该方法。如果内存紧张，系统会直接结束这个活动，而不会触发 onStop 方法。 所以保存状态信息是应该在onPause时做，而不是onStop时做。活动如果没有在前台运行，都将被停止或者Linux管理进程为了给新的活动预留足够的存储空间而随时结束这些活动。因此对于开发者来说，在设计应用程序的时候，必须时刻牢记这一原则。在一些情况下，onPause方法或许是活动触发的最后的方法，因此开发者需要在这个时候保存需要保存的信息。 </div><div align="left">&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;<strong>六、onRestart</strong> ：当处于停止状态的活动需要再次展现给用户的时候，触发该方法。 </div><div align="left">&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;<strong>七、 onDestroy </strong>：当活动销毁的时候，触发该方法。和 onStop 方法一样，如果内存紧张，系统会直接结束这个活动而不会触发该方法。 </div><div align="left">·&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;onSaveInstanceState ：系统调用该方法，允许活动保存之前的状态，比如说在一串字符串中的光标所处的位置等。 <br>
通常情况下，开发者不需要重写覆盖该方法，在默认的实现中，已经提供了自动保存活动所涉及到的用户界面组件的所有状态信息。 </div><br>
<div align="left"><strong>　<font size="4">　Activity栈</font></strong></div><br>
<div align="left">　　上面提到开发者是无法控制Activity的状态的，那Activity的状态又是按照何种逻辑来运作的呢？这就要知道 Activity 栈。<br>
　　每个Activity的状态是由它在Activity栈（是一个后进先出LIFO，包含所有正在运行Activity的队列）中的位置决定的。<br>
　　当一个新的Activity启动时，当前的活动的Activity将会移到Activity栈的顶部。<br>
　　如果用户使用后退按钮返回的话，或者前台的Activity结束，活动的Activity就会被移出栈消亡，而在栈上的上一个活动的Activity将会移上来并变为活动状态。如下图所示：</div><br>

<img id="aimg_12284" aid="12284" src="http://www.apkbus.com/data/attachment/forum/201112/07/164612fz547ovznmtmmm1z.jpg" zoomfile="data/attachment/forum/201112/07/164612fz547ovznmtmmm1z.jpg" file="data/attachment/forum/201112/07/164612fz547ovznmtmmm1z.jpg" class="zoom" onclick="zoom(this, this.src, 0, 0, 0)" width="600" inpost="1" onmouseover="showMenu({'ctrlid':this.id,'pos':'12'})" initialized="true">

<div class="tip tip_4 aimg_tip" id="aimg_12284_menu" style="position: absolute; z-index: 301; left: 619.5px; top: 2357px; display: none;" disautofocus="true" initialized="true">
<div class="xs0">
<p><strong>2.jpg</strong> <em class="xg1">(30.34 KB, 下载次数: 276)</em></p>
<p>
<a href="http://www.apkbus.com/forum.php?mod=attachment&amp;aid=MTIyODR8YTYxZGMzZDd8MTQ2MTEyOTUwNHwwfDE4MjA0&amp;nothumb=yes" target="_blank" class="gj_safe_a">下载附件</a>

</p>

<p class="xg1 y">2011-12-7 16:46 上传</p>

</div>
<div class="tip_horn"></div>
</div><br><br>
　　一个应用程序的优先级是受最高优先级的Activity影响的。当决定某个应用程序是否要终结去释放资源，Android内存管理使用栈来决定基于Activity的应用程序的优先级。<br>
　　<strong><font size="4">Activity状态</font></strong><br>
　　<strong>一般认为Activity有以下四种状态：</strong><br>
　　活动的：当一个Activity在栈顶，它是可视的、有焦点、可接受用户输入的。Android试图尽最大可能保持它活动状态，杀死其它Activity来确保当前活动Activity有足够的资源可使用。当另外一个Activity被激活，这个将会被暂停。<br>
　　暂停：在很多情况下，你的Activity可视但是它没有焦点，换句话说它被暂停了。有可能原因是一个透明或者非全屏的Activity被激活。<br>
　　当被暂停，一个Activity仍会当成活动状态，只不过是不可以接受用户输入。在极特殊的情况下，Android将会杀死一个暂停的Activity来为活动的Activity提供充足的资源。当一个Activity变为完全隐藏，它将会变成停止。<br>
　　停止：当一个Activity不是可视的，它“停止”了。这个Activity将仍然在内存中保存它所有的状态和会员信息。尽管如此，当其它地方需要内存时，它将是最有可能被释放资源的。当一个Activity停止后，一个很重要的步骤是要保存数据和当前UI状态。一旦一个Activity退出或关闭了，它将变为待用状态。<br>
　　待用： 在一个Activity被杀死后和被装在前，它是待用状态的。待用Acitivity被移除Activity栈，并且需要在显示和可用之前重新启动它。<br>
　　<strong>activity的四种加载模式</strong><br>
　　在android的多activity开发中，activity之间的跳转可能需要有多种方式，有时是普通的生成一个新实例，有时希望跳转到原来某个activity实例，而不是生成大量的重复的activity。加载模式便是决定以哪种方式启动一个跳转到原来某个Activity实例。<br>
　　在android里，有4种activity的启动模式，分别为：<br>
　　·standard: 标准模式，一调用startActivity()方法就会产生一个新的实例。<br>
　　·singleTop: 如果已经有一个实例位于Activity栈的顶部时，就不产生新的实例，而只是调用Activity中的newInstance()方法。如果不位于栈顶，会产生一个新的实例。<br>
　　·singleTask: 会在一个新的task中产生这个实例，以后每次调用都会使用这个，不会去产生新的实例了。<br>
　　·singleInstance: 这个跟singleTask基本上是一样，只有一个区别：在这个模式下的Activity实例所处的task中，只能有这个activity实例，不能有其他的实例。<br>
　　这些启动模式可以在功能清单文件AndroidManifest.xml中进行设置，中的launchMode属性。<br>
　　相关的代码中也有一些标志可以使用,比如我们想只启用一个实例,则可以使用 Intent.FLAG_ACTIVITY_REORDER_TO_FRONT 标志，这个标志表示：如果这个activity已经启动了，就不产生新的activity，而只是把这个activity实例加到栈顶来就可以了。<br>

```
Intent intent = new Intent(ReorderFour.this, ReorderTwo.class);
intent.addFlags(Intent.FLAG_ACTIVITY_REORDER_TO_FRONT);
startActivity(intent);
```
<br>
　　Activity的加载模式受启动Activity的Intent对象中设置的Flag和manifest文件中Activity的元素的特性值交互控制。<br>
　　下面是影响加载模式的一些特性<br>
　　<strong>核心的Intent Flag有：</strong><br>
<div class="quote"><blockquote>　　FLAG_ACTIVITY_NEW_TASK<br>
　　FLAG_ACTIVITY_CLEAR_TOP<br>
　　FLAG_ACTIVITY_RESET_TASK_IF_NEEDED<br>
　　FLAG_ACTIVITY_SINGLE_TOP</blockquote></div><br>
<strong>核心的特性有：</strong><br>
<div class="quote"><blockquote>　　taskAffinity<br>
　　launchMode<br>
　　allowTaskReparenting<br>
　　clearTaskOnLaunch<br>
　　alwaysRetainTaskState<br>
　　finishOnTaskLaunch</blockquote></div><br>
<strong>　四种加载模式的区别</strong><br>
　　所属task的区别<br>
　　一般情况下，“standard”和”singleTop”的activity的目标task，和收到的Intent的发送者在同一个task内，就相当于谁调用它，它就跟谁在同一个Task中。<br>
　　除非Intent包括参数FLAG_ACTIVITY_NEW_TASK。如果提供了FLAG_ACTIVITY_NEW_TASK参数，会启动到别的task里。<br>
　　“singleTask”和”singleInstance” 总是把要启动的activity作为一个task的根元素，他们不会被启动到一个其他task里。<br>
　　是否允许多个实例<br>
　　“standard”和”singleTop”可以被实例化多次，并且是可以存在于不同的task中；这种实例化时一个task可以包括一个activity的多个实例；<br>
　　“singleTask”和”singleInstance”则限制只生成一个实例，并且是task的根元素。<br>
　　singleTop 要求如果创建intent的时候栈顶已经有要创建的Activity的实例，则将intent发送给该实例，而不创建新的实例。<br>
　　是否允许其它activity存在于本task内<br>
　　“singleInstance”独占一个task，其它activity不能存在那个task里；<br>
　　如果它启动了一个新的activity，不管新的activity的launch mode 如何，新的activity都将会到别的task里运行（如同加了FLAG_ACTIVITY_NEW_TASK参数）。<br>
　　而另外三种模式，则可以和其它activity共存。<br>
　　是否每次都生成新实例<br>
　　“standard”对于每一个启动Intent都会生成一个activity的新实例；<br>
　　“singleTop”的activity如果在task的栈顶的话，则不生成新的该activity的实例，直接使用栈顶的实例，否则，生成该activity的实例。<br>
　　比如：<br>
　　现在task栈元素为A-B-C-D（D在栈顶），这时候给D发一个启动intent，如果D是 “standard”的，则生成D的一个新实例，栈变为A－B－C－D－D。<br>
　　如果D是singleTop的话，则不会生产D的新实例，栈状态仍为A-B-C-D<br>
　　如果这时候给B发Intent的话，不管B的launchmode是”standard” 还是 “singleTop” ，都会生成B的新实例，栈状态变为A-B-C-D-B。<br>
　　“singleInstance”是其所在栈的唯一activity，它会每次都被重用。<br>
　　“singleTask” 如果在栈顶，则接受intent，否则，该intent会被丢弃，但是该task仍会回到前台。 当已经存在的activity实例处理新的intent时候，会调用onNewIntent()方法，如果收到intent生成一个activity实例，那么用户可以通过back键回到上一个状态；如果是已经存在的一个activity来处理这个intent的话，用户不能通过按back键返回到这之前的状态。<br>
-----------------------------------<br>
<font size="5"><strong>二、Service详解</strong></font><br>
<br>
　　service可以在和多场合的应用中使用，比如播放多媒体的时候用户启动了其他Activity这个时候程序要在后台继续播放，比如检测SD卡上文件的变化，再或者在后台记录你地理信息位置的改变等等，总之服务嘛，总是藏在后头的。<br>
<br>
　　Service是在一段不定的时间运行在后台，不和用户交互应用组件。每个Service必须在manifest中 通过&lt;service&gt;来声明。可以通过contect.startservice和contect.bindserverice来启动。<br>
<br>
　　Service和其他的应用组件一样，运行在进程的主线程中。这就是说如果service需要很多耗时或者阻塞的操作，需要在其子线程中实现。<br>
<br>
　　service的两种模式（startService()/bindService()不是完全分离的）：<br>
<br>
<div class="quote"><blockquote>　　本地服务 Local Service 用于应用程序内部。<br>
<br>
　　它可以启动并运行，直至有人停止了它或它自己停止。在这种方式下，它以调用Context.startService()启动，而以调用Context.stopService()结束。它可以调用Service.stopSelf() 或 Service.stopSelfResult()来自己停止。不论调用了多少次startService()方法，你只需要调用一次stopService()来停止服务。<br>
<br>
　　用于实现应用程序自己的一些耗时任务，比如查询升级信息，并不占用应用程序比如Activity所属线程，而是单开线程后台执行，这样用户体验比较好。</blockquote></div><div class="quote"><blockquote>　　远程服务 Remote Service 用于android系统内部的应用程序之间。<br>
<br>
　　它可以通过自己定义并暴露出来的接口进行程序操作。客户端建立一个到服务对象的连接，并通过那个连接来调用服务。连接以调用Context.bindService()方法建立，以调用 Context.unbindService()关闭。多个客户端可以绑定至同一个服务。如果服务此时还没有加载，bindService()会先加载它。<br>
<br>
　　可被其他应用程序复用，比如天气预报服务，其他应用程序不需要再写这样的服务，调用已有的即可。</blockquote></div><br>
<div align="left"><font size="5"><strong>　生命周期</strong></font><br>
<br>
</div><div class="quote"><blockquote>使用context.startService() 启动Service是会会经历:<br>
<br>
　　context.startService() -&gt;onCreate()- &gt;onStart()-&gt;Service running<br>
<br>
　　context.stopService() | -&gt;onDestroy() -&gt;Service stop<br>
<br>
　　如果Service还没有运行，则android先调用onCreate()然后调用onStart()；如果Service已经运行，则只调用onStart()，所以一个Service的onStart方法可能会重复调用多次。<br>
<br>
　　stopService的时候直接onDestroy，如果是调用者自己直接退出而没有调用stopService的话，Service会一直在后台运行。该Service的调用者再启动起来后可以通过stopService关闭Service。<br>
<br>
　　所以调用startService的生命周期为：onCreate --&gt; onStart(可多次调用) --&gt; onDestroy</blockquote></div><div class="quote"><blockquote>　　使用使用context.bindService()启动Service会经历：<br>
<br>
　　context.bindService()-&gt;onCreate()-&gt;onBind()-&gt;Service running<br>
<br>
　　onUnbind() -&gt; onDestroy() -&gt;Service stop<br>
<br>
　　onBind将返回给客户端一个IBind接口实例，IBind允许客户端回调服务的方法，比如得到Service运行的状态或其他操作。这个时候把调用者（Context，例如Activity）会和Service绑定在一起，Context退出了，Srevice就会调用onUnbind-&gt;onDestroy相应退出。<br>
<br>
　　所以调用bindService的生命周期为：onCreate --&gt; onBind(只一次，不可多次绑定) --&gt; onUnbind --&gt; onDestory。<br>
<br>
　　在Service每一次的开启关闭过程中，只有onStart可被多次调用(通过多次startService调用)，其他onCreate，onBind，onUnbind，onDestory在一个生命周期中只能被调用一次。</blockquote></div><br>
而启动service，根据onStartCommand的返回值不同，有两个附加的模式：<br>
<br>
　　1. START_STICKY 用于显示启动和停止service。<br>
<br>
　　2. START_NOT_STICKY或START_REDELIVER_INTENT用于有命令需要处理时才运行的模式。<br>
<br>
　　服务不能自己运行，需要通过调用Context.startService()或Context.bindService()方法启动服务。这两个方法都可以启动Service，但是它们的使用场合有所不同。<br>
<br>
　　1. 使用startService()方法启用服务，调用者与服务之间没有关连，即使调用者退出了，服务仍然运行。<br>
<br>
　　如果打算采用Context.startService()方法启动服务，在服务未被创建时，系统会先调用服务的onCreate()方法，接着调用onStart()方法。<br>
<br>
　　如果调用startService()方法前服务已经被创建，多次调用startService()方法并不会导致多次创建服务，但会导致多次调用onStart()方法。<br>
<br>
　　采用startService()方法启动的服务，只能调用Context.stopService()方法结束服务，服务结束时会调用onDestroy()方法。<br>
<br>
　　2. 使用bindService()方法启用服务，调用者与服务绑定在了一起，调用者一旦退出，服务也就终止，大有“不求同时生，必须同时死”的特点。<br>
<br>
　　onBind()只有采用Context.bindService()方法启动服务时才会回调该方法。该方法在调用者与服务绑定时被调用，当调用者与服务已经绑定，多次调用Context.bindService()方法并不会导致该方法被多次调用。<br>
<br>
　　采用Context.bindService()方法启动服务时只能调用onUnbind()方法解除调用者与服务解除，服务结束时会调用onDestroy()方法。<br>
<br>
　　<strong>看看官方给出的比较流程示意图：</strong><br>
<br>
　　官方文档告诉我们，一个service可以同时start并且bind，在这样的情况，系统会一直保持service的运行状态如果service已经start了或者BIND_AUTO_CREATE标志被设置。如果没有一个条件满足，那么系统将会调用onDestory方法来终止service.所有的清理工作（终止线程，反注册接收器）都在onDestory中完成。<br>
<br>
　　拥有service的进程具有较高的优先级<br>
<br>
　　官方文档告诉我们，Android系统会尽量保持拥有service的进程运行，只要在该service已经被启动(start)或者客户端连接(bindService)到它。当内存不足时，需要保持，拥有service的进程具有较高的优先级。<br>
<br>
　　1． 如果service正在调用onCreate,onStartCommand或者onDestory方法，那么用于当前service的进程则变为前台进程以避免被killed。<br>
<br>
　　2． 如果当前service已经被启动(start)，拥有它的进程则比那些用户可见的进程优先级低一些，但是比那些不可见的进程更重要，这就意味着service一般不会被killed.<br>
<br>
　　3． 如果客户端已经连接到service (bindService),那么拥有Service的进程则拥有最高的优先级，可以认为service是可见的。<br>
<br>
　　4． 如果service可以使用startForeground(int, Notification)方法来将service设置为前台状态，那么系统就认为是对用户可见的，并不会在内存不足时killed。<br>
<br>
　　如果有其他的应用组件作为Service,Activity等运行在相同的进程中，那么将会增加该进程的重要性。<br>
<br>
　　本地service<br>
<br>
　　1.不需和Activity交互的本地服务<br>　　

```
public class LocalService extends Service {
private static final String TAG = "LocalService";
@Override
public IBinder onBind(Intent intent) {
Log.i(TAG, "onBind");
return null;
}

@Override
public void onCreate() {
Log.i(TAG, "onCreate");
super.onCreate();
}

@Override
public void onDestroy() {
Log.i(TAG, "onDestroy");
super.onDestroy();
}

@Override
public void onStart(Intent intent, int startId) {
Log.i(TAG, "onStart");
super.onStart(intent, startId);
}
}

```

Activity:<br>

```
public class ServiceActivity extends Activity {

@Override
protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);
setContentView(R.layout.servicedemo);

((Button) findViewById(R.id.startLocalService)).setOnClickListener(
new View.OnClickListener(){

@Override
public void onClick(View view) {
// TODO Auto-generated method stub
startService(new Intent("com.demo.SERVICE_DEMO"));
}
});

((Button) findViewById(R.id.stopLocalService)).setOnClickListener(
new View.OnClickListener(){

@Override
public void onClick(View view) {
// TODO Auto-generated method stub
stopService(new Intent("com.demo.SERVICE_DEMO"));
}
});
}

}
```

在AndroidManifest.xml添加：<br>

```
<service android:name=".LocalService">
<intent-filter>
<action android:name="com.demo.SERVICE_DEMO" />
<category android:name="android.intent.category.default" />
</intent-filter>
</service>
```


　否则启动服务时会提示new Intent找不到"com.demo.SERVICE_DEMO"。<br>
<br>
　　对于这类不需和Activity交互的本地服务，是使用startService/stopService的最好例子。<br>
<br>
　　运行时可以发现第一次startService时，会调用onCreate和onStart，在没有stopService前，无论点击多少次startService，都只会调用onStart。而stopService时调用onDestroy。再次点击stopService，会发现不会进入service的生命周期的，即不会再调用onCreate，onStart和onDestroy。<br>
<br>
　　而onBind在startService/stopService中没有调用。<br>
<br>
　<strong>　2.本地服务和Activity交互</strong><br>
<br>
　　对于这种case，官方的sample(APIDemo\app.LocalService)是最好的例子:<br>
<br>　

```
/**
* This is an example of implementing an application service that runs locally
* in the same process as the application. The {@link LocalServiceController}
* and {@link LocalServiceBinding} classes show how to interact with the
* service.
*
* <p>Notice the use of the {@link NotificationManager} when interesting things
* happen in the service. This is generally how background services should
* interact with the user, rather than doing something more disruptive such as
* calling startActivity().
*/
public class LocalService extends Service {
private NotificationManager mNM;

/**
* Class for clients to access. Because we know this service always
* runs in the same process as its clients, we don't need to deal with
* IPC.
*/
public class LocalBinder extends Binder {
LocalService getService() {
return LocalService.this;
}
}

@Override
public void onCreate() {
mNM = (NotificationManager)getSystemService(NOTIFICATION_SERVICE);

// Display a notification about us starting. We put an icon in the status bar.
showNotification();
}

@Override
public int onStartCommand(Intent intent, int flags, int startId) {
Log.i("LocalService", "Received start id " + startId + ": " + intent);
// We want this service to continue running until it is explicitly
// stopped, so return sticky.
return START_STICKY;
}

@Override
public void onDestroy() {
// Cancel the persistent notification.
mNM.cancel(R.string.local_service_started);

// Tell the user we stopped.
Toast.makeText(this, R.string.local_service_stopped, Toast.LENGTH_SHORT).show();
}

@Override
public IBinder onBind(Intent intent) {
return mBinder;
}

// This is the object that receives interactions from clients. See
// RemoteService for a more complete example.
private final IBinder mBinder = new LocalBinder();

/**
* Show a notification while this service is running.
*/
private void showNotification() {
// In this sample, we'll use the same text for the ticker and the expanded notification
CharSequence text = getText(R.string.local_service_started);

// Set the icon, scrolling text and timestamp
Notification notification = new Notification(R.drawable.stat_sample, text,
System.currentTimeMillis());

// The PendingIntent to launch our activity if the user selects this notification
PendingIntent contentIntent = PendingIntent.getActivity(this, 0,
new Intent(this, LocalServiceController.class), 0);

// Set the info for the views that show in the notification panel.
notification.setLatestEventInfo(this, getText(R.string.local_service_label),
text, contentIntent);

// Send the notification.
// We use a layout id because it is a unique number. We use it later to cancel.
mNM.notify(R.string.local_service_started, notification);
}
}

```

这里可以发现onBind需要返回一个IBinder对象。也就是说和上一例子LocalService不同的是，<br>
<br>
　　1. 添加了一个public内部类继承Binder，并添加getService方法来返回当前的Service对象；<br>
<br>
　　2. 新建一个IBinder对象--new那个Binder内部类；<br>
<br>
　　3. onBind方法返还那个IBinder对象。<br>
<br>
　　Activity:<br>
<br>

```
/**
* <p>Example of binding and unbinding to the {@link LocalService}.
* This demonstrates the implementation of a service which the client will
* bind to, receiving an object through which it can communicate with the service.</p>
*/
public class LocalServiceBinding extends Activity {
private boolean mIsBound;
private LocalService mBoundService;

@Override
protected void onCreate(Bundle savedInstanceState) {
super.onCreate(savedInstanceState);

setContentView(R.layout.local_service_binding);

// Watch for button clicks.
Button button = (Button)findViewById(R.id.bind);
button.setOnClickListener(mBindListener);
button = (Button)findViewById(R.id.unbind);
button.setOnClickListener(mUnbindListener);
}

private ServiceConnection mConnection = new ServiceConnection() {
public void onServiceConnected(ComponentName className, IBinder service) {
// This is called when the connection with the service has been
// established, giving us the service object we can use to
// interact with the service. Because we have bound to a explicit
// service that we know is running in our own process, we can
// cast its IBinder to a concrete class and directly access it.
mBoundService = ((LocalService.LocalBinder)service).getService();

// Tell the user about this for our demo.
Toast.makeText(LocalServiceBinding.this, R.string.local_service_connected,
Toast.LENGTH_SHORT).show();
}

public void onServiceDisconnected(ComponentName className) {
// This is called when the connection with the service has been
// unexpectedly disconnected -- that is, its process crashed.
// Because it is running in our same process, we should never
// see this happen.
mBoundService = null;
Toast.makeText(LocalServiceBinding.this, R.string.local_service_disconnected,
Toast.LENGTH_SHORT).show();
}
};

private OnClickListener mBindListener = new OnClickListener() {
public void onClick(View v) {
// Establish a connection with the service. We use an explicit
// class name because we want a specific service implementation that
// we know will be running in our own process (and thus won't be
// supporting component replacement by other applications).
bindService(new Intent(LocalServiceBinding.this,
LocalService.class), mConnection, Context.BIND_AUTO_CREATE);
mIsBound = true;
}
};

private OnClickListener mUnbindListener = new OnClickListener() {
public void onClick(View v) {
if (mIsBound) {
// Detach our existing connection.
unbindService(mConnection);
mIsBound = false;
}
}
};
}

```

<br>
　　明显看出这里面添加了一个名为ServiceConnection类，并实现了onServiceConnected(从IBinder获取Service对象)和onServiceDisconnected(set Service to null)。<br>
<br>
　　而bindService和unbindService方法都是操作这个ServiceConnection对象的。<br>
<br>
　　AndroidManifest.xml里添加:<br>
<br>
<div class="blockcode"><div id="code_F2s"><ol><li>　　&lt;service android:name=".app.LocalService" /&gt;</li></ol></div><em onclick="copycode($('code_F2s'));">复制代码</em></div>　　这里没什么特别的，因为service没有需要什么特别的action，所以只是声明service而已，而activity和普通的没差别。<br>
<br>
　　运行时，发现调用次序是这样的：<br>
<br>
　　bindService:<br>
<br>
　　1.LocalService : onCreate<br>
<br>
　　2.LocalService : onBind<br>
<br>
　　3.Activity: onServiceConnected<br>
<br>
　　unbindService: 只是调用onDestroy<br>
<br>
　　可见，onStart是不会被调用的，而onServiceDisconnected没有调用的原因在上面代码的注释有说明。<br>
<br>
<br>
------------------------<br>
<strong><font size="5">三、Broadcast Receiver详解</font></strong><br>
<br>
<br>
　　BroadcastReceiver 用于异步接收广播Intent。主要有两大类，用于接收广播的：<br>
<br>
　　·正常广播 Normal broadcasts（用 Context.sendBroadcast()发送）是完全异步的。它们都运行在一个未定义的顺序，通常是在同一时间。这样会更有效，但意味着receiver不能包含所要使用的结果或中止的API。<br>
<br>
　　·有序广播 Ordered broadcasts（用 Context.sendOrderedBroadcast()发送）每次被发送到一个receiver。所谓有序，就是每个receiver执行后可以传播到下一个receiver，也可以完全中止传播--不传播给其他receiver。 而receiver运行的顺序可以通过matched intent-filter 里面的android:priority来控制，当priority优先级相同的时候，Receiver以任意的顺序运行。<br>
<br>
　　要注意的是，即使是Normal broadcasts，系统在某些情况下可能会恢复到一次传播给一个receiver。 特别是receiver可能需要创建一个进程，为了避免系统超载，只能一次运行一个receiver。<br>
<br>
　　Broadcast Receiver 并没有提供可视化的界面来显示广播信息。可以使用Notification和Notification Manager来实现可视化的信息的界面，显示广播信息的内容，图标及震动信息。<br>
<br>
　　生命周期<br>
<br>
　　一个BroadcastReceiver 对象只有在被调用onReceive(Context, Intent)的才有效的，当从该函数返回后，该对象就无效的了，结束生命周期。<br>
<br>
　　因此从这个特征可以看出，在所调用的onReceive(Context, Intent)函数里，不能有过于耗时的操作，不能使用线程来执行。对于耗时的操作，请start service来完成。因为当得到其他异步操作所返回的结果时，BroadcastReceiver 可能已经无效了。<br>
<br>
　　发送广播<br>
<br>
　　事件的广播比较简单，构建Intent对象，可调用sendBroadcast(Intent)方法将广播发出。另外还有sendOrderedBroadcast()，sendStickyBroadcast()等方法，请查阅API Doc。<br>
<br>
　　1.new Intent with action name<br>
<br>
　　Intent intent = new Intent(String action);<br>
<br>
　　或者 只是new Intent, 然后<br>
<br>
　　intent.setAction(String action);<br>
<br>
　　2.set data等准备好了后，in activity,<br>
<br>
　　sendBroadcast(Intent); // 发送广播<br>
<br>
　　接收广播<br>
<br>
　　通过定义一个继承BroadcastReceiver类来实现，继承该类后覆盖其onReceiver方法，并在该方法中响应事件。<br>
<div class="blockcode"><div id="code_UdT"><ol><li>public class SMSReceiver extends BroadcastReceiver { <br>
</li><li><br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;@Override <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;public void onReceive(Context context, Intent intent) { <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; // get data from SMS intent <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; Bundle bundle = intent.getExtras(); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; if (bundle != null){ <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;// get message by "pdus" <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;Object[] objArray = (Object[]) bundle.get("pdus"); <br>
</li><li><br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;// rebuild SMS <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;SmsMessage[] messages = new SmsMessage[objArray.length]; <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;for (int i=0; i &lt; objArray.length; i++){ <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;messages[i] = SmsMessage.createFromPdu((byte[])objArray[i]); <br>
</li><li><br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;StringBuilder str = new StringBuilder("from: "); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;str.append(messages[i].getDisplayOriginatingAddress()); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;str.append("\nmessage:\n"); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;str.append(messages[i].getDisplayMessageBody()); <br>
</li><li><br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;Toast.makeText(context, str.toString(), Toast.LENGTH_LONG) <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;.show(); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;} <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; } <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;} <br>
</li><li>}<br>
</li><li></li></ol></div><em onclick="copycode($('code_UdT'));">复制代码</em></div>　　注册Receiver<br>
<br>
　　注册有两种方式：<br>
<br>
　　1. 静态方式，在AndroidManifest.xml的application里面定义receiver并设置要接收的action。<br>
<br>
<div class="blockcode"><div id="code_zi7"><ol><li>　　&lt;receiver android:name=".SMSReceiver"&gt;<br>
</li><li><br>
</li><li>　　&lt;intent-filter&gt;<br>
</li><li><br>
</li><li>　　&lt;action android:name="android.provider.Telephony.SMS_RECEIVED" /&gt;<br>
</li><li><br>
</li><li>　　&lt;/intent-filter&gt;<br>
</li><li><br>
</li><li>　　&lt;/receiver&gt;</li></ol></div><em onclick="copycode($('code_zi7'));">复制代码</em></div><font color="#555555"><font face="宋体"><font style="font-size:10.5pt"> 2. </font></font></font><font color="#555555"><font face="宋体"><font style="font-size:10.5pt">动态方式, 在activity里面调用函数来注册，和静态的内容差不多。一个形参是receiver，另一个是IntentFilter，其中里面是要接收的action。</font></font></font><br>
<div class="blockcode"><div id="code_X0T"><ol><li>public class HelloDemo extends Activity {&nbsp; &nbsp; <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;private BroadcastReceiver receiver;&nbsp; &nbsp; <br>
</li><li><br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;@Override <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;protected void onStart() { <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; super.onStart(); <br>
</li><li><br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; receiver = new CallReceiver(); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; registerReceiver(receiver, new IntentFilter("android.intent.action.PHONE_STATE")); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;} <br>
</li><li><br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;@Override <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;protected void onStop() { <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; unregisterReceiver(receiver); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; super.onStop(); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;} <br>
</li><li>}<br>
</li><li></li></ol></div><em onclick="copycode($('code_X0T'));">复制代码</em></div>　　一个receiver可以接收多个action的，即可以有多个intent-filter，需要在onReceive里面对intent.getAction(action name)进行判断。<br>
<br>
　　个人推荐使用静态注册方式，由系统来管理receiver，而且程序里的所有receiver，可以在xml里面一目了然。而动态注册方式，隐藏在代码中，比较难发现。<br>
<br>
　　而且动态注册，需要特别注意的是，在退出程序前要记得调用Context.unregisterReceiver()方法。一般在activity的onStart()里面进行注册, onStop()里面进行注销。官方提醒，如果在Activity.onResume()里面注册了，就必须在Activity.onPause()注销。<br>
<br>
　　Permission权限<br>
<br>
　　要接收某些action，需要在AndroidManifest.xml里面添加相应的permission。例如接收SMS:<br>
<br>
<div class="blockcode"><div id="code_r9G"><ol><li>&lt;uses-permission android:name="android.permission.RECEIVE_SMS" /&gt;</li></ol></div><em onclick="copycode($('code_r9G'));">复制代码</em></div>　　下面给出动态注册的接收来电的广播处理的CallReceiver的代码：<br>
<br>
　　一种方式是直接读取intent.getStringExtra("incoming_number")来获取来电号码：<br>
<br>
<div class="blockcode"><div id="code_x0L"><ol><li>public class CallReceiver extends BroadcastReceiver { <br>
</li><li><br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;@Override <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;public void onReceive(Context context, Intent intent) { <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; TelephonyManager teleManager = (TelephonyManager) context.getSystemService(Context.TELEPHONY_SERVICE); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;<br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; switch(teleManager.getCallState()){ <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; case TelephonyManager.CALL_STATE_RINGING: //响铃 <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;Toast.makeText(context, "Ringing: " + intent.getStringExtra("incoming_number"), Toast.LENGTH_LONG).show(); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;break; <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; case TelephonyManager.CALL_STATE_OFFHOOK: //接听 <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;Toast.makeText(context, "OffHook: " + intent.getStringExtra("incoming_number"), Toast.LENGTH_LONG).show(); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;break; <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; case TelephonyManager.CALL_STATE_IDLE: //挂断 <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;Toast.makeText(m_context, "Idle: " + incomingNumber, Toast.LENGTH_LONG).show(); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;break; <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; } <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;} <br>
</li><li>}<br>
</li><li></li></ol></div><em onclick="copycode($('code_x0L'));">复制代码</em></div>　　在运行时，发现除了响铃时可以获取来电号码，接听和挂断都不能成功获取的，显示为null。<br>
<br>
　　另一种方式是通过PhoneStateListener的onCallStateChanged来监听状态的变化：<br>
<br>
<div class="blockcode"><div id="code_Q4t"><ol><li>public class CallReceiver extends BroadcastReceiver { <br>
</li><li><br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;private Context m_context; <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;@Override <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;public void onReceive(Context context, Intent intent) { <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; m_context = context; <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; TelephonyManager teleManager = (TelephonyManager) context.getSystemService(Context.TELEPHONY_SERVICE); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; teleManager.listen(new PhoneStateListener(){ <br>
</li><li><br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;@Override <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;public void onCallStateChanged(int state, String incomingNumber) { <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;switch(state){ <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;case TelephonyManager.CALL_STATE_RINGING: //响铃 <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; Toast.makeText(m_context, "Ringing: " + incomingNumber, Toast.LENGTH_LONG) <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; .show(); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; break; <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;case TelephonyManager.CALL_STATE_OFFHOOK: //接听 <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; Toast.makeText(m_context, "OffHook: " + incomingNumber, Toast.LENGTH_LONG) <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; .show(); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; break; <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;case TelephonyManager.CALL_STATE_IDLE: //挂断 <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; Toast.makeText(m_context, "Idle: " + incomingNumber, Toast.LENGTH_LONG) <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; .show(); <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp; break; <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;} <br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;}}, PhoneStateListener.LISTEN_CALL_STATE);&nbsp;&nbsp;<br>
</li><li>&nbsp; &nbsp;&nbsp; &nbsp;&nbsp;&nbsp;} <br>
</li><li>}<br>
</li><li></li></ol></div><em onclick="copycode($('code_Q4t'));">复制代码</em></div>　　运行时也发现incomingNumber在接听和挂断时获取为blank。<br>
<br>
　　因为这里监听的是通话的状态变化，所以这个receiver会被调用3次。<br>
<br>
　　监听通话状态需要加上权限：<br>
<br>
<div class="blockcode"><div id="code_UbE"><ol><li>&lt;uses-permission android:name="android.permission.READ_PHONE_STATE"/&gt;</li></ol></div><em onclick="copycode($('code_UbE'));">复制代码</em></div>　　===========<br>
<br>
　　小结：<br>
<br>
　　1. 对于sendBroadCast的intent对象，需要设置其action name；<br>
<br>
　　2. 推荐使用显式指明receiver，在配置文件AndroidManifest.xml指明；<br>
<br>
　　3. 一个receiver可以接收多个action;<br>
<br>
　　4. 每次接收广播都会重新生成一个接收广播的对象，再次调用onReceive；<br>
<br>
　　5. 在BroadCast 中尽量不要处理太多逻辑问题，建议复杂的逻辑交给Activity 或者 Service 去处理。<br>
<br>
<br>
<br>
--------------------------------------------<br>
<strong><font size="5">四、Content Provider详解</font></strong><br>
<br>
　　ContentProvider（内容提供者）是Android中的四大组件之一。主要用于对外共享数据，也就是通过ContentProvider把应用中的数据共享给其他应用访问，其他应用可以通过ContentProvider对指定应用中的数据进行操作。ContentProvider分为系统的和自定义的，系统的也就是例如联系人，图片等数据。<br>
<br>
　　android中对数据操作包含有：<br>
<br>
　　file, sqlite3, Preferences, ContectResolver与ContentProvider前三种数据操作方式都只是针对本应用内数据，程序不能通过这三种方法去操作别的应用内的数据。<br>
<br>
　　android中提供ContectResolver与ContentProvider来操作别的应用程序的数据。<br>
<br>
　　使用方式:<br>
<br>
　　一个应用实现ContentProvider来提供内容给别的应用来操作，<br>
<br>
　　一个应用通过ContentResolver来操作别的应用数据，当然在自己的应用中也可以。<br>
<br>
　　以下这段是Google Doc中对ContentProvider的大致概述:<br>
<br>
　　内容提供者将一些特定的应用程序数据供给其它应用程序使用。内容提供者继承于ContentProvider 基类，为其它应用程序取用和存储它管理的数据实现了一套标准方法。然而，应用程序并不直接调用这些方法，而是使用一个 ContentResolver 对象，调用它的方法作为替代。ContentResolver可以与任意内容提供者进行会话，与其合作来对所有相关交互通讯进行管理。<br>
<br>
　　1.ContentProvider<br>
<br>
　　Android提供了一些主要数据类型的ContentProvider，比如音频、视频、图片和私人通讯录等。可在android.provider包下面找到一些Android提供的ContentProvider。通过获得这些ContentProvider可以查询它们包含的数据，当然前提是已获得适当的读取权限。<br>
<br>
　　主要方法：<br>
<br>
　　<font>public boolean onCreate() 在创建ContentProvider时调用</font><br>
<div class="quote"><blockquote>　　public Cursor query(Uri, String[], String, String[], String) 用于查询指定Uri的ContentProvider，返回一个Cursor<br>
<br>
　　public Uri insert(Uri, ContentValues) 用于添加数据到指定Uri的ContentProvider中<br>
<br>
　　public int update(Uri, ContentValues, String, String[]) 用于更新指定Uri的ContentProvider中的数据<br>
<br>
　　public int delete(Uri, String, String[]) 用于从指定Uri的ContentProvider中删除数据<br>
<br>
　　public String getType(Uri) 用于返回指定的Uri中的数据的MIME类型</blockquote></div><br>
　　*如果操作的数据属于集合类型，那么MIME类型字符串应该以vnd.android.cursor.dir/开头。<br>
<br>
　　例如：要得到所有person记录的Uri为content://contacts/person，那么返回的MIME类型字符串为"vnd.android.cursor.dir/person"。<br>
<br>
　　*如果要操作的数据属于非集合类型数据，那么MIME类型字符串应该以vnd.android.cursor.item/开头。<br>
<br>
　　例如：要得到id为10的person记录的Uri为content://contacts/person/10，那么返回的MIME类型字符串应为"vnd.android.cursor.item/person"。<br>
<br>
　　2.ContentResolver<br>
<br>
　　当外部应用需要对ContentProvider中的数据进行添加、删除、修改和查询操作时，可以使用ContentResolver类来完成，要获取ContentResolver对象，可以使用Context提供的getContentResolver()方法。<br>
<br>
<div class="quote"><blockquote>　　ContentResolver cr = getContentResolver();<br>
<br>
　　ContentResolver提供的方法和ContentProvider提供的方法对应的有以下几个方法。<br>
<br>
　　public Uri insert(Uri uri, ContentValues values) 用于添加数据到指定Uri的ContentProvider中。<br>
<br>
　　public int delete(Uri uri, String selection, String[] selectionArgs) 用于从指定Uri的ContentProvider中删除数据。<br>
<br>
　　public int update(Uri uri, ContentValues values, String selection, String[] selectionArgs) 用于更新指定Uri的ContentProvider中的数据。<br>
<br>
　　public Cursor query(Uri uri, String[] projection, String selection, String[] selectionArgs, String sortOrder) 用于查询指定Uri的ContentProvider。</blockquote></div><br>

<br>
　　3.Uri<br>
<br>
　　Uri指定了将要操作的ContentProvider，其实可以把一个Uri看作是一个网址，我们把Uri分为三部分。<br>
<br>
　　第一部分是"content://"。可以看作是网址中的"http://"。<br>
<br>
　　第二部分是主机名或authority，用于唯一标识这个ContentProvider，外部应用需要根据这个标识来找到它。可以看作是网址中的主机名，比如"blog.csdn.net"。<br>
<br>
　　第三部分是路径名，用来表示将要操作的数据。可以看作网址中细分的内容路径。<br>
<br>

<img id="aimg_12286" aid="12286" src="http://www.apkbus.com/data/attachment/forum/201112/07/171510b80t7v04vk8qzkty.jpg" zoomfile="data/attachment/forum/201112/07/171510b80t7v04vk8qzkty.jpg" file="data/attachment/forum/201112/07/171510b80t7v04vk8qzkty.jpg" class="zoom" onclick="zoom(this, this.src, 0, 0, 0)" width="405" inpost="1" onmouseover="showMenu({'ctrlid':this.id,'pos':'12'})">

<div class="tip tip_4 aimg_tip" id="aimg_12286_menu" style="position: absolute; display: none" disautofocus="true">
<div class="xs0">
<p><strong>1.jpg</strong> <em class="xg1">(9.25 KB, 下载次数: 283)</em></p>
<p>
<a href="http://www.apkbus.com/forum.php?mod=attachment&amp;aid=MTIyODZ8NzE2ODBmMDB8MTQ2MTEyOTUwNHwwfDE4MjA0&amp;nothumb=yes" target="_blank" class="gj_safe_a">下载附件</a>

</p>

<p class="xg1 y">2011-12-7 17:15 上传</p>

</div>
<div class="tip_horn"></div>
</div>
