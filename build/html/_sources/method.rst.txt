=================
当前可用方法介绍
=================


方法链说明
============

.. note::
	方法链是返回了其class的实例本身，可以持续调用class实例中的方法，只要是返回是self的方法，都属于支持方法链，可以进行链式操作

方法链使用示例

.. code-block:: python
	:linenos:
	:emphasize-lines: 3

	class TestDemo:
		def test_demo(self, driver):
			driver.get("https://www.baidu.com").send_keys('id', 'kw', '123')




进入网址
========

.. note::
	进入网址

.. py:function:: driver.get(url);

	:param url: 需要进入的网址
	:rtype: self


定位元素
==========

.. note::
	这是后面所有元素方法的基础，也可以单独拿出来使用，返回一个element

.. py:function:: driver.location(name, val);
	
	:param name: 元素定位方式
	:param val: 元素定位值
	:rtype: element


定位多个元素
==============

.. note::
	使用此方法可以定位多个相同属性的元素，以列表的形式进行返回

.. py:function:: driver.locations(name, val);
	
	:param name: 元素定位方式
	:param val: 元素定位值
	:rtype: element list


元素输入
=========

.. note::
	进行元素输入，设置clear为True则会替换输入框原始数据，同replace_input方法，注意的是，这里替换是模拟键盘的Ctrl+A全选，而且加入替换后，将不能输入多个数据（后续优化）

.. py:function:: driver.send_keys(name, val, txt, clear);

	:param name: 元素定位方式(xpath、id、name、css等)
	:param val: 元素值
	:param txt: 需要输入的数据
	:param clear: 布尔值，默认False，为True则替换原始数据
	:rtype: self


元素点击
=========

.. note::
	进行元素点击操作

.. py:function:: driver.click(name, val);

	:param name: 元素定位的方式
	:param val: 元素定位值
	:rtype: self


显性等待
=========

.. note::
	进行显性等待操作，等待直到元素可见可操作，使用 **wait_type** 可以选择不同的形式， **view** 代表等待元素可见， **click** 代表等待元素可点击, **no view** 等待元素消失

.. py:function:: driver.wait_for(name, val, timeout, delay, wait_type, call_back, *args， **kwargs);

	:param name: 必填，元素定位方式
	:param val: 必填，元素定位值
	:param timeout: 选填，默认10，最大等待时间
	:param delay: 选填，默认0.5，每0.5秒查看一次
	:param wait_type: 选填，等待的情况，默认'view'，可见
	:param call_back: 选填，默认None，可以选择Base实例中的方法，如send_keys、click、report_shot等元素操作
	:param args: 选填，当选择的call_back是send_keys时，或者回调的方法有其他参数时，在arg中传入
	:param kwargs: 选填，键值对传入额外需要参数
	:rtype: WebElement页面对象


自定义显性等待
================

.. note::
	当上述的显性等待不能满足selenium操作需要时，可以使用自定义显性等待，自己通过函数或者方法确定等待条件，每次会隔delay时间调用一次func函数，当返回True时判断正确，最大等待timeout时间

.. py:function:: driver.wait_custom(func, timeout, delay, reverse);

	:param func: 自定义充当条件的函数或者方法
	:param timeout: 最大等待时间，默认10
	:param delay: 做少秒查看一次，默认0.5
	:param reverse: 默认False，当为True时，当不满足条件时成立
	:rtype: WebElement/bool


强制等待
=========

.. note::
	进行强制等待操作，单位为秒，程序将阻塞填入的时间长度

.. py:function:: driver.force_wait(timeout);

	:param timeout: 需要等待的时长，整数类型，单位秒
	:rtype: self


报告截图
=========

.. note::
	对浏览器进行元素截图或者全屏截图并存入报告，如果name或者val未填写，则默认进行全屏截图，否则为元素截图

.. py:function:: driver.report_shot(name, val, picname);

	:param name: 选填，元素定位方式
	:param val: 选填，元素定位值
	:param picname: 选填，图片的名称
	:rtype: self


页面滚动
=========

.. note::
	进行页面滚动，此方法仅封装了滚动到底部和顶部的操作

.. py:function:: driver.scroll_top(top);
	
	:param top: 选填，布尔值，默认False，滚动到底部，为True时滚动到顶部
	:rtype: self


滚动到元素可见
===============

.. note::
	js进行定位操作，本质为 :ref:`执行js命令<js>` 的快捷方法

.. py:function:: driver.scroll_view(selector, back);
	
	:param selector: 定位元素值，以//开头则为xpath定位，否则为css定位
	:param back: 可选，整数类型，回滚多少像素，默认为-100，向上滚动100像素


滚动到元素可见2
================

.. note:: 
	当前是属于selenium的滚动，封装后，加入了步骤、日志记录和等待时间

.. py:function:: driver.scroll_view_element(element, back);
	
	:param element: selenium的WebElement，页面的元素
	:param back: 回滚的像素值，默认-100，即为向上滚动100像素
	:rtype: dict，返回当前元素在页面中的坐标点

创建har
========

.. note:: 
	创建har，用于捕获网页network接口数据，使用此方法，必须启用了proxy代理

.. py:function:: driver.create_har();
	
	:rtype: self
	

获取network响应
================

.. note::
	获取网页中network的数据，并以列表的形式返回

.. py:function:: driver.get_har(filter_url);

	:param filter_url: 字符串类型，指定需要过滤的网址
	:rtype: 列表list


切入iframe
============

.. note:: 
	切入到iframe的方法，如果val不填写，默认使用id、name的方式填入iframe，name则变成元素值

.. py:function:: driver.switch_iframe(name, val);

	:param name: 元素定位方式，当val为空时，name承担val职责
	:param val: 选填，元素定位值
	:rtype: self


切出iframe
============


.. note:: 
	切出iframe方法，当content为True的时候是返回主文档，默认返回上一级

.. py:function:: driver.switch_iframe_back(content);
	
	:param content: 选填，默认False，如果为True则返回主文档，否则返回上一级
	:rtype: self



切入最后一个句柄
================

.. note::
	默认切换到最后一个句柄，如果填写了参数，则以参数指定的句柄为准

.. py:function:: driver.switch_window_last(hint);

	:param hint: 选填，数字类型，选择当前的第几个句柄
	:rtype: self



获取元素属性
=============

.. note::
	定位元素并获取其属性值

.. py:function:: driver.get_attr(name, val, attr);
	
	:param name: 元素定位方式
	:param val: 元素定位值
	:param attr: 需要获取的属性名称
	:rtype: self


设置元素属性
=============

.. note::
	进行对元素的属性进行设置操作，为下面 :ref:`执行js命令<js>` 命令的简易封装


.. py:function:: driver.set_attr(selector, attr_key, attr_val);

	:param selector: 元素值，当//开头认定为xpath定位，否则为css定位
	:param attr_key: 元素属性的key值
	:param attr_val: 需要修改的属性值


移除元素属性
=============

.. note::
	删除某个元素的属性，为下面 :ref:`执行js命令<js>` 命令的简易封装

.. py:function:: driver.remove_attr(selector, attr);
	
	:param selector: 元素定位值，以//开头则认为是xpath定位，否则为css定位
	:param attr: 需要移除的元素属性


.. _js:

执行js命令
===========

.. note::
	某些场景下需要借助js语句来对页面元素进行修改等操作，可以使用此方法实现

.. py:function:: driver.execute_script(js_code);
	
	:param js_code: 需要执行的js命令块或者语句
	:rtype: 任意值


获取元素文本
=============

.. note::
	获取元素的文本

.. py:function:: driver.get_text(name, val);
	
	:param name: 元素定位方式
	:param val: 元素值
	:rtype: 字符串str


表单提交
==========

.. note::
	对于form表单，有些是可以直接进行快捷提交，而不需要去进行定位按钮操作的

.. py:function:: driver.submit(name, val);
	
	:param name: 表单的定位方式
	:param val: 表单的元素值
	:rtype: self


鼠标左键点击
=============

.. py:function:: driver.mouse_click(name, val);
	
	:param name: 元素定位方式
	:param val: 元素定位值
	:rtype: self


鼠标右键点击
=============

.. py:function:: driver.mouse_context_click(name, val);
	
	:param name: 元素定位方式
	:param val: 元素值
	:rtype: self


鼠标元素拖放
=============

.. py:function:: driver.mouse_drag(source, target);
	
	:param source: 需要进行拖放的元素，元组或者列表形式
	:param target: 目标元素，元组或者列表形式
	:rtype: self

.. warning::
	source和targe是一个 **有且仅有两个** 元素的列表或者元组，包含元素定位的方式，和元素值，第一个为定位方式，第二个值为元素值


鼠标悬浮
=========

.. note::
	鼠标悬浮在元素之上，某些元素需要进行此操作才能展示其他元素属性


.. py:function:: driver.mouse_hover(name, val);
	
	:param name: 元素定位方式
	:param val: 元素定位值
	:rtype: self


鼠标双击
=========

.. py:function:: driver.mouse_double_click(name, val);
	
	:param name: 元素定位方式
	:param val: 元素定位值
	:rtype: self


判断元素是否被选中
==================

.. warning:: 
	此方法不会抛出错误，即使找不到元素，也只会返回False，便于将其作为后续判断的条件，而不是直接异常退出

.. py:function:: driver.is_selected(name, val);
	
	:param name: 元素定位方式
	:param val: 元素定位值
	:rtype: bool布尔值


判断元素是否显示
=================

.. warning::
	此方法不会抛出异常，查找不到或者定位出错都只会返回False

.. py:function:: driver.is_displayed(name, val);

	:param name: 元素定位方式
	:param val: 元素定位值
	:rtype: 布尔值bool


判断元素是否被使用
===================

.. warning::
	此方法不会抛出异常，查找不到元素或者定位出现错误都只会返回False


.. py:function:: driver.is_enabled(name, val);

	:param name: 元素定位方式
	:param val: 元素定位值
	:rtype: 布尔值bool


断言包含元素
===============

.. note::
	断言包含的只是比较简单的断言，仅包含了在……之中，等于的结果，可以自行通过assert进行其他形式断言，但是必须在顶部加上 **with allure.step(xxx):** ，去构建一个断言步骤


.. py:function:: driver.assert_in(source, target);
	
	:param source: 需要进行断言的数据
	:param target: 目标数据


断言是否相等
==============

.. py:function:: driver.assert_equal(source, target);
	
	:param source: 需要进行断言的数据
	:param target: 目标数据


刷新当前页面
==============

.. py:function:: driver.refresh();


清空输入框
============

.. note::
	清空输入框只能针对input标签使用

.. py:function:: driver.clear_input(name, val);
	
	:param name: 元素定位方式
	:param val: 元素定位值


替换输入框数据
=================

.. note::
	当上一个清空不能使用时，可以使用此方法直接替换输入

.. py:function:: driver.replace_input(name, val, txt);

	:param name: 元素定位方式
	:param val: 元素定位值
	:param txt: 需要输入的数据




获取当前网站cookie
=====================

.. note:: 
	返回当前浏览器存放的所有cookie数据，列表形式返回

.. py:function:: driver.get_cookie();
	
	:rtype: list


获取当前页面标题
==================

.. note:: 
	标题是我们标签页上面显示的文字，可以用来查看是否进入其他页面


.. py:function:: driver.get_title();
	
	:rtype: str


获取当前页面url
================

.. note::
	需要提取当前页面的url做验证的时候，可以使用此方法

.. py:function:: driver.get_url();

	:rtype: 当前页面url


使用selenium原始driver
=========================

.. note::
	当上述方法不能满足要求时，需要临时自建方法，可以使用此方法，将返回框架所使用的driver实例，仅可读

.. py:function:: driver.origin_driver();
	
	:rtype: Webdriver.Chrome


.. code-block:: python
	:linenos:

	# 使用此方式使用原生driver的方法
	def test_xx_xx(self, driver):
		driver.origin_driver.find_element(xxx)


OCR图像识别
=============

.. note:: 
	使用此方法需要安装ddddocr模块以及其依赖，会返回识别出来的文字

.. py:function:: driver.ocr(img);

	:param img: 需要进行识别的图片路径
	:rtype: str，图像中的文字内容


预期断言
======================

.. note:: 
	预期断言需要结合循环进行，此方法省去了各种if的逻辑思考，只需要按照原来的逻辑进行断言即可，可以帮助去除逻辑分析上的思考，将精力用在更繁杂的业务功能之上。并非一定需要使用这种方式，有时候可能自己写的循环判断更简单或者更符合业务需求


.. warning::
	预期断言会忽略你代码中的所有错误，直到断言成功或者超出循环次数，超出循环次数则会抛出异常，所以你不需要在你的代码中加入异常处理


.. py:function:: driver.wait_assert(rounds, current_round, driver=None);
	
	:param rounds: 循环总次数，与外部循环总次数对应
	:param current_round: 当前循环次数
	:param driver: 选填，使用的driver对象，此框架中为Base实例，传入则默认获取一次成功或者失败图片保存到报告中


 **下面演示了其基本使用方式：**


.. code-block:: python
	:linenos:

	def test_xxx(self, driver):
	    for i in range(10):
	        with driver.wait_assert(10, i, driver) as e:
	            if e:
	                break
	            time.sleep(2)
	            xxxxxxxx
	            xxxxxxxx
	            assert xx == xx


.. warning::
	此方法必须是一个能抛出错误的方法，错误交由with给定的内部程序去处理只需要关注业务逻辑，如果循环次数用完未通过，则会抛出错误，如果使用if的形式，想使用此方法，也需要将非理想数据raise出来
	你需要自己加上每次循环的间隔，如上面每次进行真正业务逻辑前，都会等待2秒
	在很多时候，你可能会需要加上统计计时：

.. code-block:: python
	:linenos:

	def test_xxx(10):
	    use_time = 你设置的初始时间
	    for i in range(10):
	        with driver.wait_assert(10, i, driver) as e:
	            if e:
	                break
	            time.sleep(2)
	            xxxxxxxxxxxx
	            xxxxxxxxxxxx
	            assert xx == xx
	        use_time += 2
	    allure.attach(
	        f'第{r}次获取请求成功断言，原定拦截时间{data1}秒，总等待耗时{user_time}秒',
	        name='循环断言成功',
	        attachment_type=allure.attachment_type.TEXT
	    )


关闭当前标签页
===============

.. py:function:: driver.close_window();

