<h2>Adapter</h2>
<h3>1. Adapter概念解析</h3>
<h4>1.1 Adapter继承结构图</h4>

![](http://www.runoob.com/wp-content/uploads/2015/09/77919389.jpg)

<font color="ff0000">开发中常用到的Adapter</font><br>

<blockquote><ul>
<li><strong>BaseAdapter</strong>：抽象类，实际开发中我们会继承这个类并且重写相关方法，用得最多的一个Adapter！</li>
<li>ArrayAdapter：支持泛型操作，最简单的一个Adapter，只能展现一行文字~</li>
<li>SimpleAdapte：同样具有良好扩展性的一个Adapter，可以自定义多种效果！</li>
<li>SimpleCursorAdapter：用于显示简单文本类型的listView，一般在数据库那里会用到，不过有点过时，
不推荐使用！</li>
</ul>
</blockquote>

<h3>2 自定义BaseAdapter</h3>
继承BaseAdapter，重写<strong>getView()</strong>、getCount()、getItem()、getItemId()方法。
<br><br>
<font color="ff0000">示例:</font><br>

```
public class AnimalAdapter extends BaseAdapter {

    private LinkedList<Animal> mData;
    private Context mContext;

    public AnimalAdapter(LinkedList<Animal> mData, Context mContext) {
        this.mData = mData;
        this.mContext = mContext;
    }

    @Override
    public int getCount() {
        return mData.size();
    }

    @Override
    public Object getItem(int position) {
        return null;
    }

    @Override
    public long getItemId(int position) {
        return position;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        convertView = LayoutInflater.from(mContext).inflate(R.layout.item_list_animal,parent,false);
        ImageView img_icon = (ImageView) convertView.findViewById(R.id.img_icon);
        TextView txt_aName = (TextView) convertView.findViewById(R.id.txt_aName);
        TextView txt_aSpeak = (TextView) convertView.findViewById(R.id.txt_aSpeak);
        img_icon.setBackgroundResource(mData.get(position).getaIcon());
        txt_aName.setText(mData.get(position).getaName());
        txt_aSpeak.setText(mData.get(position).getaSpeak());
        return convertView;
    }
}
```

<h3>3 BaseAdapter的优化</h3>
<h4>3.1 复用ConvertView</h4>
<li><Strong>优化前的代码：</strong>界面上有多少个Item，那么getView方法就会被调用多少次。getView()代码：
<br><br>
<font color="ff0000">示例:</font><br>

```
@Override
public View getView(int position, View convertView, ViewGroup parent) {
    convertView = LayoutInflater.from(mContext).inflate(R.layout.item_list_animal,parent,false);
    ImageView img_icon = (ImageView) convertView.findViewById(R.id.img_icon);
    TextView txt_aName = (TextView) convertView.findViewById(R.id.txt_aName);
    TextView txt_aSpeak = (TextView) convertView.findViewById(R.id.txt_aSpeak);

    img_icon.setBackgroundResource(mData.get(position).getaIcon());
    txt_aName.setText(mData.get(position).getaName());
    txt_aSpeak.setText(mData.get(position).getaSpeak());
    return convertView;
}
```
<li><Strong>优化后的代码：</strong>减少inflater的调用次数，判断convertView不为空，则复用。getView()代码：

<br><br>
<font color="ff0000">示例:</font><br>

```
@Override
public View getView(int position, View convertView, ViewGroup parent) {

    if(convertView == null){
        convertView = LayoutInflater.from(mContext).inflate(R.layout.item_list_animal,parent,false);
    }

    ImageView img_icon = (ImageView) convertView.findViewById(R.id.img_icon);
    TextView txt_aName = (TextView) convertView.findViewById(R.id.txt_aName);
    TextView txt_aSpeak = (TextView) convertView.findViewById(R.id.txt_aSpeak);

    img_icon.setBackgroundResource(mData.get(position).getaIcon());
    txt_aName.setText(mData.get(position).getaName());
    txt_aSpeak.setText(mData.get(position).getaSpeak());
    return convertView;
}
```

<h4>3.2 ViewHolder重用组件</h4>
减少findViewById()的调用次数，<strong>优化有的代码</strong>：
<br><br>
<font color="ff0000">示例:</font><br>

```
@Override
public View getView(int position, View convertView, ViewGroup parent) {
    ViewHolder holder = null;
    if(convertView == null){
        convertView = LayoutInflater.from(mContext).inflate(R.layout.item_list_animal,parent,false);
        holder = new ViewHolder();
        holder.img_icon = (ImageView) convertView.findViewById(R.id.img_icon);
        holder.txt_aName = (TextView) convertView.findViewById(R.id.txt_aName);
        holder.txt_aSpeak = (TextView) convertView.findViewById(R.id.txt_aSpeak);
        convertView.setTag(holder);   //将Holder存储到convertView中
    }else{
        holder = (ViewHolder) convertView.getTag();
    }
    holder.img_icon.setBackgroundResource(mData.get(position).getaIcon());
    holder.txt_aName.setText(mData.get(position).getaName());
    holder.txt_aSpeak.setText(mData.get(position).getaSpeak());
    return convertView;
}

static class ViewHolder{
    ImageView img_icon;
    TextView txt_aName;
    TextView txt_aSpeak;
}
```
