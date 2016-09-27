<h2>ListView</h2>
<h3>1. ListView的概念</h3>略
<h3>2. ListView的焦点问题</h3>

方法1：为抢占了控件的组件设置：android：focusable="false"<br>

方法2：item根节点设置：android:descendantFocusability="blocksDescendants"
<blockquote>
<ul><li>
beforeDescendants：viewgroup会优先其子类控件而获取到焦点
</li>
<li>
afterDescendants：viewgroup只有当其子类控件不需要获取焦点时才获取焦点
</li>
<li>
blocksDescendants：viewgroup会覆盖子类控件而直接获得焦点
</li>
</ul>
</blockquote>

<h3>3. ListView的错位问题</h3>
listView中getView的方法机制<br><br>
![](http://www.runoob.com/wp-content/uploads/2015/09/23101560K-0.jpg)

原因：采用ViewHolder进行加载时，加载过程是ViewHolder是复用的，而且是异步的过程，就会导致显示上的错位和闪烁。<br>

<strong>解决办法：</strong>给每个有可能发生复用或者闪烁的view设置一个tag，然后在set的时候进行判断，
是否是当前item的View

<h3>4. ListView的数据更新问题</h3>
<h4>4.1 数据为空</h4>
setEmptyView(View)方法，当ListView数据为空的时候， 显示一个对应的View。
<h4>4.2 增加或者删除一条数据</h4>
修改Adapter中数据后，再notifyDataSetChanged();
<h4>4.2 修改一条数据</h4>
<ul>
<li>找到对应的item进行重绘
<li>notifyDataSetChanged()方法会判断是否需要重新渲染，如果当前item没有必要重新渲染 是不会重新渲染的，
如果某个Item的状态发生改变，都会导致View的重绘，
而重绘的并不是 所有的Item，而是View状态发生变化的那个Item！所以我们直接notifyDataSetChange()方法 即可。</ul>

<h3>5. 构建一个可复用的自定义BaseAdapter</h3>
<strong>Step1:</strong>将entity改为泛型<br><br>
<font color="ff0000">示例</font>

```
public class MyAdapter<T> extends BaseAdapter {

    private Context mContext;
    private LinkedList<T> mData;

    public MyAdapter() {
    }

    public MyAdapter(LinkedList<T> mData, Context mContext) {
        this.mData = mData;
        this.mContext = mContext;
    }

    ....
}
```

<strong>Step2:</strong>优化ViewHolder<br><br>
<blockquote>
ViewHolder用来保存item的中控件的状态（findViewById）,我们这里将getView的大部分逻辑写入ViewHolder的类中。
<ul><li>定义一个查找控件的方法，调用方法时传递过来的id，以及设置的内容，比如：

`
 public ViewHolder setText(int id, CharSequence text)
`

<li>将convertView复用部分搬到这里，那就需要传递一个context对象了，我们把需要获取 的部分都写到构造方法中！
<li>写一堆设置方法(public)，比如设置文字大小颜色，图片背景等！
</blockquote>

一、相关参数和构造方法：

```
public static class ViewHolder {

    private SparseArray<View> mViews;   //存储ListView 的 item中的View
    private View item;                  //存放convertView
    private int position;               //游标
    private Context context;            //Context上下文

    //构造方法，完成相关初始化
    private ViewHolder(Context context, ViewGroup parent, int layoutRes) {
        mViews = new SparseArray<>();
        this.context = context;
        View convertView = LayoutInflater.from(context).inflate(layoutRes, parent,false);
        convertView.setTag(this);
        item = convertView;
    }

    ImageView img_icon;
    TextView txt_content;
}
```

二、绑定ViewHolder与Item

```
//绑定ViewHolder与item
public static ViewHolder bind(Context context, View convertView, ViewGroup parent,
                              int layoutRes, int position) {
    ViewHolder holder;
    if(convertView == null) {
        holder = new ViewHolder(context, parent, layoutRes);
    } else {
        holder = (ViewHolder) convertView.getTag();
        holder.item = convertView;
    }
    holder.position = position;
    return holder;
}
```

三、根据Id获取集合中的控件

```
public <T extends View> T getView(int id) {
    T t = (T) mViews.get(id);
    if(t == null) {
        t = (T) item.findViewById(id);
        mViews.put(id, t);
    }
    return t;
}
```

四、定义ViewHolder中暴露出来的方法

```
/**
 * 设置文字
 */
public ViewHolder setText(int id, CharSequence text) {
    View view = getView(id);
    if(view instanceof TextView) {
        ((TextView) view).setText(text);
    }
    return this;
}

/**
 * 设置图片
 */
public ViewHolder setImageResource(int id, int drawableRes) {
    View view = getView(id);
    if(view instanceof ImageView) {
        ((ImageView) view).setImageResource(drawableRes);
    } else {
        view.setBackgroundResource(drawableRes);
    }
    return this;
}

/**
 * 设置点击监听
 */
public ViewHolder setOnClickListener(int id, View.OnClickListener listener) {
    getView(id).setOnClickListener(listener);
    return this;
}

/**
 * 设置可见
 */
public ViewHolder setVisibility(int id, int visible) {
    getView(id).setVisibility(visible);
    return this;
}

```

<strong>Step3:</strong>定义一个抽象的方法，完成ViewHolder和Data的数据绑定<br>

`
public abstract void bindView(ViewHolder holder, T obj);
`


<strong>Step4:</strong>修改getView()部分的内容<br>
```
@Override
public View getView(int position, View convertView, ViewGroup parent) {
    ViewHolder holder = ViewHolder.bind(parent.getContext(), convertView, parent, mLayoutRes
            , position);
    bindView(holder,getItem(position));
    return holder.getItemView();
}
```

<strong>Step5:</strong>BaseApater的初始化及应用<br>

```
...

//Adapter初始化
        myAdapter1 = new MyAdapter<App>((ArrayList)mData1,R.layout.item_one) {
            @Override
            public void bindView(ViewHolder holder, App obj) {
                holder.setImageResource(R.id.img_icon,obj.getaIcon());
                holder.setText(R.id.txt_aname,obj.getaName());
            }
        };
        myAdapter2 = new MyAdapter<Book>((ArrayList)mData2,R.layout.item_two) {
            @Override
            public void bindView(ViewHolder holder, Book obj) {
                holder.setText(R.id.txt_bname,obj.getbName());
                holder.setText(R.id.txt_bauthor,obj.getbAuthor());
            }
        };

        //ListView设置下Adapter：
        list_book.setAdapter(myAdapter2);
        list_app.setAdapter(myAdapter1);
```

<h3>6. ListView多布局的实现</h3>
重写getItemViewType()方法对应View是哪个类别，以及getViewTypeCount()方法返回
总共多少个类别！然后再getView那里调用getItemViewType获得对应类别，再加载对应的View！<br>

<font color="ff0000">示例</font>

```
//多布局的核心，通过这个判断类别
   @Override
   public int getItemViewType(int position) {
       if (mData.get(position) instanceof App) {
           return TYPE_APP;
       } else if (mData.get(position) instanceof Book) {
           return TYPE_BOOK;
       } else {
           return super.getItemViewType(position);
       }
   }

   //类别数目
   @Override
   public int getViewTypeCount() {
       return 2;
   }


   @Override
   public View getView(int position, View convertView, ViewGroup parent) {
       int type = getItemViewType(position);
       ViewHolder1 holder1 = null;
       ViewHolder2 holder2 = null;
       if(convertView == null){
          switch (type){
              case TYPE_APP:
                  holder1 = new ViewHolder1();
                  convertView = LayoutInflater.from(mContext).inflate(R.layout.item_one, parent, false);
                  holder1.img_icon = (ImageView) convertView.findViewById(R.id.img_icon);
                  holder1.txt_aname = (TextView) convertView.findViewById(R.id.txt_aname);
                  convertView.setTag(R.id.Tag_APP,holder1);
                  break;
              case TYPE_BOOK:
                  holder2 = new ViewHolder2();
                  convertView = LayoutInflater.from(mContext).inflate(R.layout.item_two, parent, false);
                  holder2.txt_bname = (TextView) convertView.findViewById(R.id.txt_bname);
                  holder2.txt_bauthor = (TextView) convertView.findViewById(R.id.txt_bauthor);
                  convertView.setTag(R.id.Tag_Book,holder2);
                  break;
          }
       }else{
           switch (type){
               case TYPE_APP:
                   holder1 = (ViewHolder1) convertView.getTag(R.id.Tag_APP);
                   break;
               case TYPE_BOOK:
                   holder2 = (ViewHolder2) convertView.getTag(R.id.Tag_Book);
                   break;
           }
       }

       Object obj = mData.get(position);
       //设置下控件的值
       switch (type){
           case TYPE_APP:
               App app = (App) obj;
               if(app != null){
                   holder1.img_icon.setImageResource(app.getaIcon());
                   holder1.txt_aname.setText(app.getaName());
               }
               break;
           case TYPE_BOOK:
               Book book = (Book) obj;
               if(book != null){
                   holder2.txt_bname.setText(book.getbName());
                   holder2.txt_bauthor.setText(book.getbAuthor());
               }
               break;
       }
       return convertView;
   }


   //两个不同的ViewHolder
   private static class ViewHolder1{
       ImageView img_icon;
       TextView txt_aname;
   }

   private static class ViewHolder2{
       TextView txt_bname;
       TextView txt_bauthor;
   }
```

<h3>7. ListView的headerView、footerView和emptyView</h3>
通过自定义listView实现带上拉加载、下拉刷新，带有header头和bottom底部的listView。
<h4>7.1 listView 的headerView</h4>
<blockquote>
<ul>
<li>addHeaderView（）方法：主要是向listView的头部添加布局<br>addHeaderView(headView,null,false)区别是添加的布局
是否可点击。
<li>addFooterView()方法必须放在listview.setadapter前面。
<li>public void onItemSelected(AdapterView<?> parent, View view, int position, long id)从headview开始算起
<li>headerViewd的隐藏方法有：setPadding(0,-h,0,0)或者remove（）、addView（）
</ul>
</blockquote>
<h4>7.2 listView 的footerView</h4>

<h4>7.3 listView 的emptyView</h4>

<h3>8. ListView的常用第三方控件（下拉刷新，上拉更多）</h3>
<li>https://github.com/Maxwin-z/XListView-Android
<li>https://github.com/shontauro/android-pulltorefresh-and-loadmore
<li>https://github.com/liaohuqiu/android-Ultra-Pull-To-Refresh【2980上使用的】
