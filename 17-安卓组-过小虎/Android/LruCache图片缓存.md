<font size = "4">

[toc]

### 什么是LruCache图片缓存
我们在Android中加载一张图片十分简单，但是如果我们要加载一大推图片呢？基于这个问题我们引入LruCache类提供缓存

### LruCache的使用方法
1. 构造函数：接收一个int型数据，注意LruCache需要指明泛型<string , bitmap>用于存储bitmap，在读取的时候通过这个string键值来读取
```
long maxMemory = Runtime.getRuntime().maxMemory();
int cacheSize = (int) (maxMemory / 8);
//计算需要的最大内存
lruCache = new LruCache<String, Bitmap>(cacheSize) {
    @Override
    protected int sizeOf(String key, Bitmap value) {
        return value.getByteCount();
    }
    //重写sizeof方法用于safeSizeof计算已缓存大小
};
```
2. put(String key， V value)：将需要缓存的内容放入缓存区
3. safeSizeof：用来返回已经缓存的大小
4. get(String key)：通过键值返回缓存中的内容
5. remove(K key)：从缓存区删除内容，并更新已缓存大小

注意：LruCache有一个需要我们重写的方法，就是sizeof(String key, V value)，这个函数在safeSizeof计算已缓存的空间时候会调用


</font>