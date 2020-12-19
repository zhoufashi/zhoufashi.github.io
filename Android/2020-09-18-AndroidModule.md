```
<intent-filter>
	指定 Activity、服务或广播接收器可以响应的 Intent 类型	
	包含于：
		<activity>
		<activity-alias>
		<service>
		<receiver>  
	必须包含：<action>
	可包含：
		<category>
		<data>
	
<action>
		android:name 操作的名称
		
		
<activity>
	包含它的文件：
		<application>
	可包含：
		<intent-filter>
		<meta-data>
		<layout>
	说明：
		声明实现应用部分可视化界面的 Activity（一个 Activity 子类）。必须用清单文件中的 <activity> 元素表示所有 Activity。系统不会识别和运行任何未进行声明的 Activity。
			
<activity-alias>
	包含于：
		<application>
	可包含：
		<intent-filter>
		<meta-data>
	说明：
		Activity 的别名，由 targetActivity 属性命名。目标必须与别名在同一应用中，并且在清单中必须在别名之前进行声明。
		别名将目标 Activity 呈现为独立实体。它可以具有自己的一组 Intent 过滤器，这些 Intent 过滤器（而不是目标 Activity 本身的 Intent 过滤器）决定了哪些 Intent 可以通过别名激活目标，以及系统如何处理别名。例如，别名的 Intent 过滤器可以指定“android.intent.action.MAIN”和“android.intent.category.LAUNCHER”标志，以使其呈现在应用启动器中，即使目标 Activity 本身的任何过滤器都未设置这些标志。
			
			
<application>
	应用的声明。此元素包含用于声明每个应用组件的子元素，并且具有会影响所有组件的属性
	包含于：
		<manifest>
	可包含：
		<activity>
		<activity-alias>
		<meta-data>
		<service>
		<receiver>
		<provider>
		<uses-library>
			
<category>
	语法：
		<category android:name="string" />
	包含于：
		<intent-filter>
	说明：
		向 Intent 过滤器添加类别名称。如需详细了解 Intent 过滤器和类别规范在过滤器中的作用，请参阅 Intent 和 Intent 过滤器。
			
<data>
	包含于：
		<intent-filter>
	说明：
		向 Intent 过滤器添加数据规范。该规范可以是只有数据类型（mimeType 属性），可以是只有 URI，也可以是既有数据类型又有 URI。
			
<instrumentation>
	包含于：
		<manifest>
	说明：
		声明用于监控应用与系统交互的 Instrumentation 类。Instrumentation 对象在应用的所有组件之前进行实例化。

<manifest>
	包含于：
		无
	必须包含：
		<application>
	可包含：
		<compatible-screens>
		<instrumentation>
		<permission>
		<permission-group>
		<permission-tree>
		<supports-gl-texture>
		<supports-screens>
		<uses-configuration>
		<uses-feature>
		<uses-permission>
		<uses-permission-sdk-23>
		<uses-sdk>
	说明：
		AndroidManifest.xml 文件的根元素。它必须包含 <application> 元素并指定 xmlns:android 和 package 属性。

<meta-data>
	包含于：
		<activity>
		<activity-alias>
		<application>
		<provider>
		<receiver>
		<service>
	说明：
		可以向父组件提供的其他任意数据项的名称值对。

<permission>
	包含于：
		<manifest>
	说明：
		声明可用于限制对此应用或其他应用的特定组件或功能的访问权限的安全权限

<provider>
	包含于：
		<application>
	可包含：
		<meta-data>
		<grant-uri-permission>
		<path-permission>
	说明：
		声明内容提供程序组件.内容提供程序是 ContentProvider 的子类，可提供对由应用管理的数据的结构化访问机制。应用中的所有内容提供程序都必须在清单文件的 <provider> 元素中定义；否则，系统将不知道它们，也不会运行它们。

<receiver>
	包含于：
		<application>
	可包含：
		<intent-filter>
		<meta-data>
	说明：
		将广播接收器（BroadcastReceiver子类）声明为应用的组件之一。广播接收器允许应用接收由系统或其他应用广播的 Intent，即使应用的其他组件并没有运行也是如此。
		
<service>
	包含它的文件：
		<application>
	可包含：
		<intent-filter>
		<meta-data>
	说明：
		将服务（Service 子类）声明为应用的一个组件。与 Activity 不同，服务缺少可视化界面。服务用于实现长时间运行的后台操作，或可由其他应用调用的富通信 API。

<uses-configuration>
	包含于：
		<manifest>
	说明：
		指示应用所需的硬件和软件功能

<supports-screens>
    包含于：
		<manifest>
	说明：
		使您能够指定应用支持的屏幕尺寸，并为比应用支持的最大屏幕还大的屏幕启用屏幕兼容模式。

<supports-gl-texture>
	包含于：
		<manifest>
	说明：
		声明应用支持的一种 GL 纹理压缩格式。

<uses-feature>
	包含它的文件：
		<manifest>
	说明：
		声明应用使用的单个硬件或软件功能。

<uses-library>
	包含于：
		<application>
	说明：
		指定应用必须与之关联的共享库。此元素告知系统将库的代码添加到软件包的类加载器中。


<uses-permission>
	包含它的文件：
		<manifest>
	说明：
		指定用户必须授予的系统权限，以便应用正常运行

<uses-sdk>
	包含它的文件：
		<manifest>
	说明：
		您可以通过整数形式的 API 级别表示应用与一个或多个版本的 Android 平台的兼容性



```


[返回2](../) 






