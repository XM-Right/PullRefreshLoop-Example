这是一个以《猫眼电影》中，下拉加载切出的并闪动的效果作为参考，来实现这样的一个加载模块。这个其中切出的边线效果是由原生去实现的，所以这个模块我们只需要传入中心图标即可。此分享我也就照葫芦画瓢把模拟猫眼作为实例分享给大家。大家可以借鉴通过做出更多炫酷的类似效果。

按照官方对此模块的概述，所以这里我使用了 window + frame 的布局，如果你只是使用在独立的 window 布局，那么就需要在 config.xml 中配置 <preference name="customRefreshHeader' value="模块名称'/>。

1. 在 index.html 中使用 openFrame 打开 main.html，这个地方需要特别注意，此模块与其他模块引入方式不同，是不需要使用 require 去引用的，只需要在打开 openFrame 时，在其配置中新增 customRefreshHeader 字段即可，此字段接收一个字符串，因为使用 pullRefreshLoop 模块，所以填写模块名就行。
	
2. 在 main.html 初始化的 apiready 时使用 setCustomRefreshHeaderInfo 方法初始化好它的 UI( 当然你可以在任何你需要的时候在初始化加载 UI )，该方法接收两个值，即参数与刷新完成后的回调。参数中的 icon 字符串字段就是下拉过程的中心展示图标，下拉会有一个固定的最大高度，在下拉小于最大高度的这个过程，图标周围会有一个随着高度切出的边线，需要注意的是为了保证图标居中以及不存在变形和失真的情况，官方文档推荐使用 50*50、100*100 尺寸图片。

3. 当下拉为刷新加载状态时，会触发 setCustomRefreshHeaderInfo 方法的回调，这时就需要你去回调中做你的数据逻辑，最后当你确定数据加载完成，则调用 refreshHeaderLoadDone 方法结束加载，我这里用 3 秒定时器代替数据加载。

4. 很多场景需要程序自动刷新，所以此模块也提供了 refreshHeaderLoading 方法，具体效果你下载源码来试试。