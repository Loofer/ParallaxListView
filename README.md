## ParallaxListView 带有视差动画的listview

![带视差的 ListView][https://github.com/Loofer/ParallaxListView/blob/master/screen/parallaxlistview.gif]

## 用法

* xml 文件
```

    <org.loofer.parallaxlistview.ParallaxListView
        android:id="@+id/listview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

```

* activity
```

      listview = (ParallaxListView) findViewById(R.id.listview);

        listview.setOverScrollMode(ListView.OVER_SCROLL_NEVER);//永远不显示蓝色阴影

        //添加header
        View headerView = View.inflate(this,R.layout.layout_header, null);
        ImageView imageView = (ImageView) headerView.findViewById(R.id.imageView);
        listview.setParallaxImageView(imageView);

        listview.addHeaderView(headerView);
		
        listview.setAdapter(new ArrayAdapter<String>(this,android.R.layout.simple_list_item_1, indexArr));

```

### 原理

* 继承 ListView

    在构造方法中给 Header 中的 ImageView 设置监听 addOnGlobalLayoutListener 获取图片的高度

* 重写 overScrollBy 方法（在listview滑动到头的时候执行，可以获取到继续滑动的距离和方向）

    在 overScrollBy 方法中根据情况给 ImageView 设置高度

* 重写 onTouchEvent 方法

    ev.getAction() == MotionEvent.ACTION_UP 当手指抬起，时利用 ValueAnimator 设置 ImageView 缩小动画，并添加弹性差之器

