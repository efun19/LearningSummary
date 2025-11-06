## View

### Menu

#### 选项菜单

在Activity中重写onCreatePanelMenu方法加载menu

```java
@Override
public boolean onCreatePanelMenu(int featureId, @NonNull Menu menu) {
    getMenuInflater().inflate(R.menu.main, menu);
    return true;
}
```

在Activity中重写onOptionsItemSelected方法处理menu点击事件

```Java
@Override
public boolean onOptionsItemSelected(@NonNull MenuItem item) {
    int itemId = item.getItemId();
	...
    return super.onOptionsItemSelected(item);
}
```

#### 自定义Toolbar

##### ActionBar

如果使用setSupportActionBar使Toolbar成为系统的ActionBar，会让 `Activity` 来管理其生命周期和菜单，则必须通过重写onCreatePanelMenu、onOptionsItemSelecte方法来加载控制menu

##### 非ActionBar

如果不调用 `setSupportActionBar()`，而是将Toolbar作为一个独立的视图来管理菜单，那么可以通过toolbar.inflateMenu()、toolbar.setOnMenuItemClickListener方法来加载控制
