```
Activity跳转方式总结
一、显式调用方法
1.方法一
 Intent intent=new Intent(本类，将要跳转的类);   //Intent intent=new Intent(MainActivity.this,JumpToActivity.class);   
 startActivity（intent）；
 
2.方法二：
Intent intent2=new  Intent();
intent2.setClass(本类，将要跳转的类);   // intent2.setClass(MainActivity.this,JumpToActivity.class);
startActivity（intent2）;

2.方法三：
Intent intent2=new  Intent();
intent2.setComponent(new ComponentName(MainActivity.this, JumpToActivity.class));
//component，目标组件的包或类名称（完整类名）：以下几种形式
//.setComponent(new ComponentName(getApplicationContext(), JumpToActivity.class));
//intent.setComponent(new ComponentName(getApplicationContext(), "com.liujc.test.JumpToActivity"));
//intent.setComponent(new ComponentName("com.liujc.test", "com.liujc.test.JumpToActivity"));
startActivity（intent2）;

二：隐式调用方法

1.通过action跳转：
Intent intent = new Intent();  
intent.setAction("con.liujc.test.jump");  
startActivity(intent);
需要将要跳转到的Activity在AndroidManifest.xml中设置action:
<activity android:name=".JumpToActivity" >  
    <intent-filter>  
        <action android:name="con.liujc.test.jump"/>  
        <category android:name="android.intent.category.DEFAULT" />  
    </intent-filter>  
</activity>

2.通过Scheme跳转协议跳转：
 android中的scheme是一种页面内跳转协议，是一种非常好的实现机制，通过定义自己的scheme协议，可以非常方便跳转app中的各个页面；通过scheme协议，服务器可以定制化告诉App跳转那个页面，可以通过通知栏消息定制化跳转页面，可以通过H5页面跳转页面等。
URL Scheme协议格式：
scheme://host:port/path ** 　　模式://主机:端口/路径**
完整的URL Scheme协议格式：liujc://goods:8080/goodsDetail?goodsId=20170112
上面的路径 Scheme、Host、port、path、query全部包含:
liujc代表该Scheme 协议名称
goods代表Scheme作用于哪个地址域
goodsDetail代表Scheme指定的页面
goodsId代表传递的参数
8080代表该路径的端口号
URL Scheme如何使用：
 (1).在AndroidManifest.xml中对<activity />标签增加<intent-filter />设置Scheme:
 <activity
            android:name=".GoodsDetailActivity"
            android:theme="@style/AppTheme">
            <!--要想在别的App上能成功调起App，必须添加intent过滤器-->
            <intent-filter>
                <!--协议部分，随便设置-->
                <data android:scheme="liujc" android:host="goods" android:path="/goodsDetail" android:port="8080"/>
                <!--下面这几行也必须得设置-->
                <category android:name="android.intent.category.DEFAULT"/>
                <action android:name="android.intent.action.VIEW"/>
                <category android:name="android.intent.category.BROWSABLE"/>
            </intent-filter>
        </activity>
		
  (2).获取Scheme跳转的参数:
     Uri uri = getIntent().getData();
     if (uri != null) {
    // 完整的url信息
    String url = uri.toString();
    Log.e(TAG, "url: " + uri);
    // scheme部分
    String scheme = uri.getScheme();
    Log.e(TAG, "scheme: " + scheme);
    // host部分
    String host = uri.getHost();
    Log.e(TAG, "host: " + host);
    //port部分
    int port = uri.getPort();
    Log.e(TAG, "host: " + port);
    // 访问路劲
    String path = uri.getPath();
    Log.e(TAG, "path: " + path);
    List<String> pathSegments = uri.getPathSegments();
    // Query部分
    String query = uri.getQuery();
    Log.e(TAG, "query: " + query);
    //获取指定参数值
    String goodsId = uri.getQueryParameter("goodsId");
    Log.e(TAG, "goodsId: " + goodsId);
    }
     (3).调用方式:
	  网页上:（使用系统自带浏览器或者谷歌浏览器）
     <a href="liujc://goods:8080/goodsDetail?goodsId=20170112">打开商品详情</a>
    原生调用：
	 Intent intent = new Intent(Intent.ACTION_VIEW,Uri.parse("liujc://goods:8080/goodsDetail?goodsId=20170112")); 
      startActivity(intent);
	  
	  (4).如何判断一个Scheme是否有效,有效后再启动:
	PackageManager packageManager = getPackageManager();
	Intent intent = new Intent(Intent.ACTION_VIEW, Uri.parse("liujc://goods:8080/goodsDetail?goodsId=20170112"));
	List<ResolveInfo> activities = packageManager.queryIntentActivities(intent, 0);
	boolean isValid = !activities.isEmpty();
	if (isValid) {
		startActivity(intent);
	}
	
	
	
@string/app_name指的是定义在strings.xml中的app_name
开发什么组件用作应用程序中的一部分，都需要在应用程序项目根目录下的manifest.xml文件中声明所有的组件


解决图片失真的问题  
android:scaleType="fitXY"
android:background="#e0000000

按钮背景
android:background="@null"
```

[返回](../) 