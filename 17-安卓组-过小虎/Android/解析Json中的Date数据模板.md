<font size = "4">

当后台服务器需要向我们传送一个时间的时候就会使用SQL类型中的Date数据
这个数据并不会像一个String一样单纯的传送过来，

而是一个包含了时间信息的JsonObject类。这个类包含了很多信息，第一次解析的时候很懵逼

```
{"date":22,"day":1,"hours":20,"minutes":42,"month":3,"seconds":53,"time":1555936973000,"timezoneOffset":-480,"year":119}
```

看到这样的数据我也不知道该怎么解析，后来发现通过毫秒数也就是"time"这个key可以获取到毫秒数，并通过循环获取到年月日
```

JSONObject time = jsonObject.getJSONObject("admissionTime");
long t1 = time.getLong("time");

//


public static String getJsonTime(long time){
    Date date = new Date();
    date.setTime(time);
    SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd");
    return simpleDateFormat.format(date);
}
```
</font>