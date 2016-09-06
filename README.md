# -iOS-

移动APP的开发相比传统的项目迭代周期要短很多，需求的变化也频繁一些，在开发工作中采用合适的架构可以有效的节约开发时间，提高开发效率。本文档总结了杭州市民卡APP iOS客户端正在使用的架构模式。\n

一、架构目录\n
整个架构目录分以下部分：\n

1、	Src文件夹主要用来编码实现过程中使用到的公共类、自定义控件、自定义逻辑判断方法和各个功能模块。\n

1）、Common目录用来存放APP公用的图片资源文件，预定义宏文件和自定义适合本APP的viewController文件，之后使用到的viewController都可以继承与它，这样可以统一UI样式，快捷的调用统一的网络连接方法等。
2）、Component目录用来存放封装好的一些自定义控件。

这些自定义的控件，按照设计好的样式进行封装。使用时，只要简单的初始化，代入基本的参数，就可以快速的实现UI控件的实现。可以有效的减少代码量，减少硬编码，同时是代码更加的清晰，便于阅读。
3）、Business目录用来管理存放各个功能模块的实现。

以市民卡APP个人中心为例，在个人中心目录中，分解模块功能分别建立对应的目录，同时一些图片资源文件根据模块的需要分别存放在对应的UI目录中。这样便于资源文件的管理，和分模块的维护。
2、	SMKThirdli目录主要用于存放使用到的第三方方法和库。
主要集成了杭州市民卡支付SDK、加密键盘、SDWebImage、MBHUD提示框、AFNetworking网络连接方式等。
能存放到这个目录下的第三方方法和库都必须是使用度广泛，还在维护或者便于我们自己修改的，这样能保障APP的稳定，确保性能的可靠。
3、	SMKFrameworks目录用来存放app的系统文件。Appdelegate文件和app的info.plist文件存放于此。
4、	Frameworks目录存放apple自带的系统资源库。

二、命名规则
市民卡APP iOS框架的命名规则必须与功能名称相一致。
自定义控件命名：
SMK+控件名。比如SMKButton、SMKLabel、SMKTextfield等。
功能模块命名：
SMK+视图名+功能名。比如校园健身登记，SMKFitnessRegisterViewController。
模块目录名称可以使用中文。代码中必须有注释说明。
方法名必须避免词不达意，方法名、变量名尽量用最简单的术语说明。能用英语表述尽量用英文，允许少量的拼音。
三、SMKBaseViewController文件介绍
SMKBaseViewController继承于UIViewController，此类包含了网络请求方法，各个页面跳转方法，hud显示和友盟UV、PV统计方法。
1、	网络请求方法
网络请求在AFNetworking第三方库基础上进行封装。AFNetworking3.0底层基于苹果最新网络请求方法NSURLSession，支持ipv6，使用异步请求方法。相对于停止维护的ASIHTTPREQUEST更稳定，同时更新维护也比较方便。


2、	hud提示框显示
hud提示框基于现在使用最广泛的MBHUD第三方库封装，使用简单，扩展性强。
-(void)hudDissmiss;//提示框小时
-(void)ShowWarningHud:(NSString *)message;//显示警告类提示框，后面参数填写警告语
-(void)ShowHud:(NSString *)message;//显示一半类型的提示框，后面参数填写提示语
-(void)ShowWarningHudMid:(NSString *)message;//在页面中间显示提示框，后面参数填写警告语
3、	友盟统计方法：
友盟统计方法用于每个页面的用户跟踪和使用时长的统计。方便相关同事进行对APP用户数和模块使用度的统计。
-(void)tongjiUV:(NSString *)viewName;//统计用户访问数，后面参数填写模块名称
-(void)tongjiCount:(NSString *)actionName;//统计特定的操作数，后面的参数填写对应的操作名。
4、	页面挑战方法：
-(void)pushToNextViewController:(UIViewController *)viewController;//跳转下一页面
-(void)backView;//返回上一页面
-(void)backToRootView;//返回根页面
-(void)backToIndexView:(int)index;//返回到指定页面
四、SmkConfigDefine宏定义文件说明
宏定义可以很方便开发和调试，我们也要对其进行归类，提高代码可读性和规范性。宏定义在很多方面都会使用，例如定义高度、判断iOS系统、工具类，还有诸如文件路径、服务端api接口文档。为了对宏能够快速定位和了解其功能，我们最好在定义的时候将其放入特定的头文件中，
宏命名规范以小写字母k开头，后面跟上宏名称。
SmkConfigDefine.h文件中包含了市民卡APP常用的宏。获取屏幕宽、高度；各个网络请求链接；各个空间属性设置；获取设备信息；第三方授权key等。
五、自定义控件说明:
1、SMKNoNetWorkView：无网络或者网络请求失败是显示的页面。提供重新请求网络操作。
2、SMKLabel：继承UILabel类，封装了label常用的方法，使用的时候只要传入相应的参数就可以。
3、SMKButton：继承UIButton类，封装了button常用的方法，使用的时候只要传入相应的参数就可以。
4、SMKTextField：继承UItextField类，封装了textField常用的方法，使用的时候只要传入相应的参数就可以。SMKTextField样式分三类：一、输入框前是图片；二、输入框前是文字；三、基本样式
5、SMKWebView：继承UIWebView类，可以跟踪到页面的跳转顺序，按app的返回键返回对应的网页。


