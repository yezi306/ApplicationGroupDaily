Gallery画廊可以实现拖动查看照片的功能。

1. 准备适配器Adapt
```
public float getScale(boolean focused, int offset){
    return Math.max(0, 1.0f/(float)Math.pow(2, Math.abs(offset)));
}
//在适配器中使用该方法测量距中央的位移量，利用getScale返回View的大小
```
2. 如同ListView一样装配适配器
```
setAdapter(new ImageAdapt(this));
```

