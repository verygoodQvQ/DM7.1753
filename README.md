# DM7.1753
大漠7.1753破解版

【内部版本使用须知】
1. 内部版本的驱动后台是后台的终极实现，所以大家一定要避免此版本和文档外泄.
2. 使用此版本，必须把插件改名，比如xxx.dll等. 不要直接用dm.dll. 如果插件不改名，创建对象会失败.
3. 软件提示中不要有任何暴露插件信息的提示. 比如含有大漠或者插件等的字眼.
4. 内部版本默认是不开启错误提示的。如果想要错误提示，手动调用SetShowErrorMsg 1
5. 内部版本在简单游平台使用时，不会在简单游平台扣费，必须要注册，通过我的计费系统使用.
6. 插件的对象名字修改为xml.parste. 原来代码里的所有创建对象dm.dmsoft的地方都要换成此对象名. 比如set dm = createobject("xml.parste")
7. 大家的利益大家共同维护，谢谢!
8. 简单游平台如果要使用内部版本，请自己后台审核一下插件。 或者想办法绕过上传插件机制。

内部版本相比普通版本 增加了以下功能, 其他功能和说明和普通版本一致.
1. 驱动后台
2. DmGuard中的pass盾 h1 hd和h3盾


1. 驱动后台(目前仅支持32位平台。)
BindWindowEx函数中增加了以下属性 
鼠标: 
drv.mouse.position.lock.api相对应dx.mouse.position.lock.api 功能和说明和普通版本保持一致. 
drv.mouse.clip.lock.api相对应dx.mouse.clip.lock.api 功能和说明和普通版本保持一致. 
drv.mouse.input.lock.api相对应dx.mouse.input.lock.api 功能和说明和普通版本保持一致. 
drv.mouse.state.api相对应dx.mouse.state.api 功能和说明和普通版本保持一致. 
drv.mouse.cursor相对应dx.mouse.cursor 功能和说明和普通版本保持一致. 
drv.mouse.input.lock.api2相对应dx.mouse.input.lock.api2 功能和说明和普通版本保持一致. 
drv.mouse.input.lock.api3相对应dx.mouse.input.lock.api3 功能和说明和普通版本保持一致. 
drv.mouse.raw.input相对应dx.mouse.raw.input功能和说明和普通版本保持一致. 
键盘:
drv.keypad.input.lock.api相对应dx.keypad.input.lock.api 功能和说明和普通版本保持一致. 
drv.keypad.state.api相对应dx.keypad.state.api 功能和说明和普通版本保持一致. 
drv.keypad.raw.input相对应dx.keypad.raw.input 功能和说明和普通版本保持一致. 
公共:
drv.public.active.api相对应dx.public.active.api 功能和说明和普通版本保持一致. 

当使用驱动后台属性时，绑定的模式必须是201 203中的一个.


具体模式的组合方式大家可以到VIP绑定测试工具中测试。

需要注意的是: 驱动后台中为了节省系统资源，最多同时被绑定的进程数量不可以超过64个.

2. DmGuard  pass盾功能和说明. 
"pass [pid]" : 允许指定进程可以过以下列表中的驱动保护. pid为可选参数.如果不指定pid，默认当前进程.(此模式需要加载驱动,目前仅支持32位系统)
比如
dm.DmGuard 1,"pass"
dm.DmGuard 1,"pass 3408"
dm.DmGuard 1,"pass 96"

允许过的驱动保护函数如下:
【SSDT】
NtOpenProcess
NtOpenThread
NtOpenSection
NtProtectVirtualMemory
NtReadVirtualMemory
NtWriteVirtualMemory
NtQueryVirtualMemory

NtLoadDriver
NtQueryInformationProcess
NtMapViewOfSection


NtCreateProcess
NtCreateProcessEx
NtCreateThread
NtCreateThreadEx
NtCreateSection

NtCreateDebugObject
NtDebugActiveProcess
NtDebugContinue
NtTerminateProcess
NtTerminateThread

【SSDT Shadow】
NtUserMessageCall
NtUserPostMessage
NtUserQueryWindow

注: pass盾和驱动后台功能都会让绝大多数安全软件失效。 要重新生效必须重启系统. 另外这2个驱动可能会和部分安全软件冲突。
使用此功能，最好是先关闭安全软件，以免无故蓝屏. 

另注: 经过测试发现驱动和360浏览器有冲突,有很大几率会蓝屏。建议使用驱动后台不要安装360的任何产品.

当驱动后台绑定失败时,GetLastError的错误描述增加如下
-30 64位系统
-31 驱动释放失败 
-32 驱动加载失败 



2. DmGuard  h1盾功能和说明. 
此盾用来保护后台不被检测. (特别对apex很有效)
此盾配合后台绑定时，后台参数里不可以有dx.public.graphic.protect 可能会导致防检测失效.

3. DmGuard  hd盾功能和说明. 
此盾用来虚拟硬盘序列号和mac
硬盘序列号和mac保证一个进程一个结果,也可以自己指定一个机器码.
但mac的只适用于2003和xp 其他系统没作用。  
硬盘的所有系统都可以

用法:
清空白名单
dm.DmGuard 1,"hd cls"
增加一个白名单,(即指定的进程可以获取正确的机器码),如果有指定多个白名单,多次调用即可
dm.DmGuard 1,"hd w 0" '把自身进程名加到白名单
dm.DmGuard 1,"hd w 1.exe"
dm.DmGuard 1,"hd w 22.exe"
指定机器码,后面这个数字不同，则对应的机器码也不同，即一个数字一个机器码.
dm.DmGuard 1,"hd const 123"
dm.DmGuard 1,"hd const 124"
dm.DmGuard 1,"hd const 200"
等等


4. GetInfo说明
// 这个返回当前Reg的账户余额
yue = dm.GetInfo("yu","") 


5. DmGuard  h3盾功能和说明. 
此盾用来隐藏目录和文件,同时保护目录和文件不被非法访问.
用法:
清空保护列表，黑名单，白名单
dm.DmGuard 1,"h3 cls"
增加一个保护目录(这个目录包括这个目录所有的子目录和文件都被隐藏和保护),如果要保护多个,就多次调用即可
dm.DmGuard 1,"h3 p 0" '这个是保护当前dll所在的目录
dm.DmGuard 1,"h3 p 1" '这个是保护当前进程所在的目录
dm.DmGuard 1,"h3 p c:\TestDir"
dm.DmGuard 1,"h3 p c:\TestDir2"
dm.DmGuard 1,"h3 p d:\testDir3"
等等
增加一个白名单,(即指定的进程可以随意访问保护的目录),注意,开启h3盾的进程是默认加到白名单进程的. 如果有指定多个白名单,多次调用即可
注意,白名单只有在黑名单为空时才起作用
dm.DmGuard 1,"h3 w explorer.exe" '这个可以让资源管理器里看到你的目录
dm.DmGuard 1,"h3 w regsvr32.exe" '这个可以让你的DLL顺利注册
等等
增加一个黑名单,(即除了指定的进程,都可以随意访问保护的目录),如果有指定多个黑名单,多次调用即可
注意,如果添加了黑名单,那么白名单将失效.
dm.DmGuard 1,"h3 b explorer.exe" '这个可以让资源管理器里看不到你的目录,但其他进程可以
dm.Dmguard 1,"h3 b qq.exe"
等等


6. DmGuard vv盾功能和说明
此盾仅仅是模拟BIOS中关闭Intel-Vt或者Amd-Svm功能. 适合于某些老的主板，默认开了VT，但又无法关闭.
某些保护系统会利用VT做保护,如果无法手动关闭VT，可以考虑使用这个盾.
调用方法
dm.DmGuard 1,"vv"
此盾目前版本很少会用到


7. DmGuard pg盾功能和说明
此盾过windows pg保护


8. DmGuard phide phide2 phide3
和普通版本说明一致，但在64位系统上调用此盾，必须先过pg保护
