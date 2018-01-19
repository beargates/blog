webview内核版本39.0.0.0.0
1. 兼容性问题常出现在华为系列手机

2. iphone 行高跟其他手机表现不一致
     1）普通文字的行高；iphone和其他手机的默认行高不一致；例如想要在div中居中其子元素“<span>文字</span>”，此时必须控制文字的行高
     2）input的行高；直接影响光标的高度

3. focus事件
     iphone不允许开发者主动让input等主动focus，即el.focus()；在iphone上不会生效;
    据说允许通过click等点击事件获取焦点，如el1.click = (){el2.focus()}

4. autoprefixer-loader遗漏的(v3.2.0)
     A.类似transition: transform(...) scale(...)多种变换时，需手动处理前缀
     B. ios 7.0.3 flex-shrink, align-items, justify-content属性需要手动处理兼容性, 且display: flex要多加（display: -webkit-flex）做兼容

5. input readonly disabled区别

6. 关于display：flex
    1)
     <div style="display:flex">
          <div style="display:flex">
               <i>icon</i>
               <div id="text" style="text-overflow:ellipsis">very long text</div>
          </div>
     </div>
     结果：webview里面非常长的文本会正常显示省略号，而在pc端chrome里则不会，文本会溢出

     猜测：可能是flex里再嵌套flex带来的bug

     处理：给＃text加样式｛width：1px｝（宽度不会表现为1px）

    2)给button使用display：flex
        在firefox（50.1.0）上不会生效
        在safari（10.0）上 justify-content不生效

    解决办法：给button里面加一个div，给div设置flex；或者直接用div替换button（不考虑语义化）

7.关于box-shadow
    在safari上 x-offset如果是负值（即超出父元素），阴影不会显示
