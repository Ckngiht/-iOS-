# -iOS-
杭州市民卡iOS APP架构
整个架构分一下几块：
1、SMKBaseViewController类。该类继承与ViewController，是所有视图控制器的父类。在该类包含了一些通用的方法和UI的样式。
通用方法包括：
1、	本地数据存储的封装。
2、	友盟数据统计方法的封装
3、	页面跳转方法的封装。
4、	不同类型提示框的封装。
5、	网络连接方法的封装。
6、	报文数据的加、解密方法封装
UI样式包括：
1、	导航栏基本样式
2、	导航栏返回样式
2、SmkConfigDefine.h头文件，主要用于预定义宏的封装。一些全局的方法，只要在此文件中修改对应值，就可以让所有使用到该方法的类都改变。
3、SMKnoNetWorkView类，用于无网络情况下，页面的显示，包含再次请求网络的操作。
4、SMKLabel类，是对UILabel常用方法的封装，通过封装好的方法，快速集成label类，减少了代码量，同时方便维护。
5、SMKButton类，是在杭州市民卡APP Button UI样式的基础上，进行UIButton封装，让在APP中使用到的button类，都具有一致性。同时增加了对button的二次封装，不用样式，使用不用的方法，方便程序员使用。
6、SMKLineView类，是在杭州市民卡APP View UI样式的基础上，进行二次封装。增加了分割线，统一每一个view的显示方式。
7、SMKTextfield类，是在杭州市民卡APP textfield UI样式的基础上，进行二次封装。分成图片样式的textfield，和纯文字的textfield，不同类型对应不同的模式。
