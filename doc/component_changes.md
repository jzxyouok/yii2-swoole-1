* yii\di\Container yii的核心组件容器,重写以针对类读取控制,后期扩展热部署支持
* yii\web\Application 改变了bootstrap方式,初始化阶段不再运行BootStrapInterface->bootstrap方法.延迟在run方法中,防止一些初始化问题
* yii\web\Response 替换该组件以使用swoole的输出,可以启用以支持大文件
* yii\web\ErrorHandle 代码中包含了exit语法,因此需要重写.
* yii\web\Session 取消初步化注册php关闭,session需要显示在配置文件中声明,才可识别.如果swoole对session的不完全支持,如session_set_cookie_params,session无法写入
* yii\log\Logger Exception不能被序列化,需要重写log的实现,在日志配置需要注意exportInterval,根据服务器环境设置

> 默认启用了自动组件替换,如果你自己定义了组件,请在启动脚本中初始化Container后,关闭autoReplace