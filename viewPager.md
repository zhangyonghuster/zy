<h2>ViewPager</h2>
<h3>1. ViewPager概念</h3>
<strong>ViewPager</strong>就是一个简单的页面切换组件，我们可以往里面填充多个View,然后我们可以左右滑动，
从而切换不同的View,我们也可以通过setPageTransformer()方法为我们的ViewPager设置切换时的动画。
<li>Google官方是建议使用Fragment来填充ViewPager的。
<h4>1.1 PagerAdapter</h4>
<li><strong>PagerAdapter
<li>FragmentPagerAdapter
<li>FragmentStatePagerAdapter</strong>
PagerAdapter和FragmentPagerAdapter一样，只会缓存当前的Fragment以及左边一个和右边一个，即总共三个。

<h4>1.2 PagerAdapter的使用</h4>
继承PagerAdapter，重写以下四个方法：
<li>getCount():获取ViewPager中有多少个View
<li>destoryItem():移除给定位置的页面
<li>instantiateItem():将给定位置的view添加到ViewGroup，并且返回新界面的Obiect（key）对象，带有key值。
<li>isViewFromObject():判断当前View是否正确，reutrn view==object
<br><br>
<font color="ff0000">示例</font>

```
public class MyPagerAdapter extends PagerAdapter {
    private ArrayList<View> viewLists;

    public MyPagerAdapter() {
    }

    public MyPagerAdapter(ArrayList<View> viewLists) {
        super();
        this.viewLists = viewLists;
    }

    @Override
    public int getCount() {
        return viewLists.size();
    }

    @Override
    public boolean isViewFromObject(View view, Object object) {
        return view == object;
    }

    @Override
    public Object instantiateItem(ViewGroup container, int position) {
        container.addView(viewLists.get(position));
        return viewLists.get(position);
    }

    @Override
    public void destroyItem(ViewGroup container, int position, Object object) {
        container.removeView(viewLists.get(position));
    }
}
```

<h4>1.3 PagerAdapter的优化</h4>
ViewPager虽然每次都预加载左中右三个View，但是在切换时，只会重新向左或者向又重新加载一个View并且销毁一个View，所以我们
联想到ListView中BaseAdapter的用法，这里使用缓存存储一个View。(试用于View布局相同的情况，如图片的切换)<br>
<br>
<font color="ff0000">流程</font>
<blockquote>
<li>overwrite <strong>destroyItem(ViewGroup container, int position,
Object view)</strong> ans save you cached view
<li>create a separate method to see if there is any chance to use a recycled
view or should you inflate a new one.
<li>remember to remove the recycled view from cache once its been used to avoid
having same view attaching same view to the pager.</blockquote>
<font color="ff0000">示例</font>

```
private View inflateOrRecycleView(Context context)
{

    View viewToReturn;
    mInflater = LayoutInflater.from(context);
    if (mRecycledViewsList.isEmpty())
    {
        viewToReturn = mInflater.inflate(R.layout.fragment_dates_grid_page, null, false);
    }
    else
    {
        viewToReturn = mRecycledViewsList.pop();
        Log.i(TAG,"Restored recycled view from cache "+ viewToReturn.hashCode());
    }


    return viewToReturn;
}

@Override
public void destroyItem(ViewGroup container, int position, Object view)
{
    VerticalViewPager pager = (VerticalViewPager) container;
    View recycledView = (View) view;
    pager.removeView(recycledView);
    mRecycledViewsList.push(recycledView);
    Log.i(TAG,"Stored view in cache "+ recycledView.hashCode());
}
```
