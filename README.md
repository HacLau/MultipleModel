MultipleModel
=============

A library to create multiple item view fast. It is used in [DragTopLayout](https://github.com/chenupt/DragTopLayout) and [SpringIndicator](https://github.com/chenupt/SpringIndicator).

#Usage
Add the dependency to your build.gradle.
```
dependencies {
    compile 'com.github.chenupt.android:multiplemodel:2.0.1@aar'
}
```
### ListView & GridView & Spinner e.t.c

Just use [ModelListAdapter](https://github.com/chenupt/MultipleModel/blob/master/lib%2Fsrc%2Fmain%2Fjava%2Fgithub%2Fchenupt%2Fmultiplemodel%2FModelListAdapter.java) which extends BaseAdapter.

```
ModelListAdapter adapter = new ModelListAdapter(this, getModelManagerBuilder());
listView.setAdapter(adapter);
```
The getModelManagerBuilder() is used for creating a [ViewManager]() to setup your all item view types.
You could return a ViewManager like this:
```
public ViewManager getModelManagerBuilder(){
        return ViewManager
        .begin()
        .addModel(CustomView.class) // The class is one of your item view type.
        .addModel(CustomLargeView.class);
}
```
Now we can add some data to the adapter. Use ItemEntityUtil to create a ItemEntity to a list and set the adapter finally.
```
    public List<ItemEntity> getTestList(){
        List<ItemEntity> resultList = new ArrayList<ItemEntity>();
        for (int i = 0; i < testStrings.length; i++) {
            // testStrings[i] is some data you want to set this item so you could use when bindview.
            ItemEntityUtil.create(testStrings[i]).setModelView(CustomView.class).attach(resultList);
        }
        for (int i = 0; i < testStrings.length; i++) {
            ItemEntityUtil.create(testStrings[i]).setModelView(CustomLargeView.class).attach(resultList);
        }
        return resultList;
    }


    // finally set it to your adapter.
    adapter.addList(getTestList());
    adapter.notifyDataSetChanged();
```

### ViewPager

Use [ModelPagerAdapter](https://github.com/chenupt/MultipleModel/blob/master/lib%2Fsrc%2Fmain%2Fjava%2Fgithub%2Fchenupt%2Fmultiplemodel%2Fviewpager%2FModelPagerAdapter.java) which extends FragmentPagerAdapter.
```
ModelPagerAdapter adapter = new ModelPagerAdapter(getSupportFragmentManager(), getModelPagerManager());
viewPager.setAdapter(adapter);
```
The same way to get a PagerManager:
```
    private PagerManager getModelPagerManager(){
        List<ItemEntity> list = new ArrayList<ItemEntity>();
        for (int i = 0; i < titles.length; i++) {
            ItemEntityUtil.create(titles[i]).setModelView(ItemFragment.class).attach(list);
        }
        return PagerManager.begin().addFragments(list).setTitles(titles);
    }
```
Developed By
---
 * Chenupt - <chenupt@gmail.com>
 * G+ [chenupt](https://plus.google.com/u/0/109194013506774756478)
 * 微博：[chenupt](http://weibo.com/p/1005052159173535/home)
 * QQ：753785666

License
---

    Copyright 2015 chenupt

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.


