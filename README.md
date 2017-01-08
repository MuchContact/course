# Selenium课程培训
1. 课前准备：
	* 环境准备
		- 安装Java1.8
		- 安装Intellij IDEA(社区版即可)  [下载地址](https://www.jetbrains.com/idea/)
		- 安装gradle [下载地址](https://gradle.org/gradle-download/)
		- 安装chrome
		- 下载chrome webdriver [下载地址](https://chromedriver.storage.googleapis.com/index.html?path=2.27/)
	* 资料预习
		- [Selenium文档](https://github.com/SeleniumHQ/selenium)
		- [selenium 1.0和selenium 2.0区别](http://www.jianshu.com/p/4f0930c0b6a8)
1. 培训安排
	1. 环境配置和例子展示
		- 目标：熟悉Selenium API
		- 时间：30min
		- 开发语言：Java
		- 使用例子的正确姿势：
			* 下载[Demo Project](https://github.com/MuchContact/EgovaMobileTest)
			* 修改`EgovaMobileTest/src/test/java/MobileServerTest.java`中`System.setProperty("webdriver.chrome.driver", "/Users/muco/Software/chromedriver")`的路径配置。例如chromedriver.exe放置在c:/Users/muco/, 则修改为`System.setProperty("webdriver.chrome.driver", "c:/Users/muco/chromedriver.exe")`
			* 添加gradle到path
			* 在工程目录路径下执行gradle test，无报错说明环境配置ok
	1. 课堂实践（3人一组共同完成以下任务）

	任务：
		1. 完成登录测试
		1. 完成产品列表测试

	时间要求：30min

	1. 拓展
	  * 自动化测试在调试中的应用
	  * 使用自动化测试接口实现微信自动发送消息 [查看](https://github.com/MuchContact/appium.wechat)
