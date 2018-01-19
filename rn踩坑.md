1. 给Text设置boderRadius不生效，外层需包个View

2. 像素网格对齐
在iOS设备上，你可以给元素指定任意精度的坐标和尺寸，例如29.674825。不过最终的物理屏幕上只会显示固定的坐标数。譬如iPhone4的分辨率是640x960，而iPhone6是750*1334。iOS会试图尽可能忠实地显示你指定的坐标，所以它采用了一种把一个像素分散到多个像素里的做法来欺骗眼睛。但这个作用的负面影响是显示出来的元素看起来会有一些模糊。
在实践中，我们发现开发者们并不想要这个特性，反而需要去做一些额外的工作来确保坐标与像素坐标对齐，来避免元素显得模糊。在React Native中，我们会自动对齐坐标到像素坐标。
我们做这个对齐的时候必须十分小心。如果你同时使用已经对齐的值和没有对齐的值，就会很容易产生一些因为近似导致的累积错误。即使这样的累积错误只发生一次，后果也可能会很严重，因为很可能会导致一个像素宽的边框最终突然消失或者显示为两倍的宽度。
在React Native中，所有JS中的东西，包括布局引擎，都使用任意精度的数值。我们只在主线程最后设置原生组件的位置和坐标的时候才去做对齐工作。而且，对齐是相对于屏幕进行的，而非相对于父元素进行，进一步避免近似误差的累积。

3. 可以通过以下方式让input获取焦点
<TextInput ref={ref => this.input = ref} />
this.input.focus()

4. 引用https://github.com/ivpusic/react-native-image-crop-picker选择照片插件时
用react-native link了该包
结果xcode中RCTDefines.h文件找不到
unlink 之后 才能解除 pod引用的包，否则即便podFile中删除了，依然会引用

5. 让input focus
<TextInput ref={ref => this.input = ref} />
this.input.focus()

6. headerTitleStyle：设置导航条文字样式。安卓上如果要设置文字居中，只要添加alignSelf:'center'就可以了。在安卓上会遇到，如果左边有返回箭头导致文字还是没有居中的问题，最简单的解决思路就是在右边也放置一个空的按钮。
http://www.jianshu.com/p/2f575cc35780

7. 从A跳转到B，然后关闭A页面

8. TextInput android 没有onKeyPress事件

9. android上 border不会应用opacity属性

10. 猜测：页面间传递数据（setParams）可能导致安卓上页面跳转/返回卡顿

11. Toast.info(successMsg, 1, () => this.props.navigation.goBack(null));
这种写法会导致连续返回两次（魅族M463c android4.4.4）

12. <View style={{padding: 10}}><Image style={{position: 'absolute', top: -6, right: -6}}/></View>
这种情况下 在安卓上top：-6部门的图片会被切割掉；
如果父View设置成margin，则在ios上会同样被切掉；
image改成position：relative有同样问题，zIndex也不生效

13. 问题说明：在更新了安卓app某个版本之后，actionsheet和图片预览都不好用了，
猜测是因为他们共同使用了Modal，Modal没有被正确调用
