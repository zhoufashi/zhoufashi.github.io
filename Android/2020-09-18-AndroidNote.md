`
Activity 类是 Android 应用的关键组件，而 Activity 的启动和组合方式则是该平台应用模型的基本组成部分。
Activity 提供窗口供应用在其中绘制界面
	
Activity 生命周期
	onCreate() 初始化 Activity 
	onStart() 进入“已启动”状态
	onResume() 
	onPause()被覆盖之类（可见）
	onStop() 不可见,做资源回收
	onRestart() 按下home键的调用
	onDestroy() 销毁
按下home()之后，再次进入到当前activity的时候调用。
调用顺序onPouse()->onStop()->onRestart()->onStart()->onResume()
当AActivity切换BActivity的所执行的方法：
	AActivity:onCreate()->onStart()->onResume()->onPouse()
	BActivity:onCreate()->onStart()->onResume()
	AActivity:onStop()->onDestory()
```