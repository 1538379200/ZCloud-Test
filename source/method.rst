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


元素输入
=========

.. note::
	进行元素输入

.. py:function:: driver.send_keys(name, val, txt);

	:param name: 元素定位方式(xpath、id、name、css等)
	:param val: 元素值
	:param txt: 需要输入的数据
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
	进行显性等待操作，等待直到元素可见可操作

.. py:function:: driver.wait_for(name, val, timeout, delay, call_back, *args);

	:param name: 必填，元素定位方式
	:param val: 必填，元素定位值
	:param timeout: 选填，默认10，最大等待时间
	:param delay: 选填，默认1，每1秒查看一次
	:param call_back: 选填，默认None，可以选择Base实例中的方法，如send_keys、click、report_shot等元素操作
	:param args: 选填，当选择的call_back是send_keys时，或者回调的方法有其他参数时，在arg中传入
	:rtype: self



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

.. py:function:: driver.report_shot(name, val);

	:param name: 选填，元素定位方式
	:param val: 选填，元素定位值
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
	目前仅支持使用css进行定位操作，本质为 :ref:`执行js命令<js>` 的快捷方法

.. py:function:: driver.scroll_view(selector);
	
	:param css_selector: 定位元素值，以//开头则为xpath定位，否则为css定位，selector内部应仅使用单引号


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

	:param selector: 元素值，当//开头认定为xpath定位，否则为css定位，selector内部都应仅使用单引号
	:param attr_key: 元素属性的key值
	:param attr_val: 需要修改的属性值


移除元素属性
=============

.. note::
	删除某个元素的属性，为下面 :ref:`执行js命令<js>` 命令的简易封装

.. py:function:: driver.remove_attr(selector, attr);
	
	:param selector: 元素定位值，以//开头则认为是xpath定位，否则为css定位，selector内部应仅使用单引号
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

.. py:function:: driver.is_selected(name, val);
	
	:param name: 元素定位方式
	:param val: 元素定位值
	:rtype: bool布尔值


判断元素是否显示
=================

.. py:function:: driver.is_displayed(name, val);

	:param name: 元素定位方式
	:param val: 元素定位值
	:rtype: 布尔值bool


判断元素是否被使用
===================

.. py:function:: driver.is_enabled(name, val);

	:param name: 元素定位方式
	:param val: 元素定位值
	:rtype: 布尔值bool


关闭当前标签页
===============

.. py:function:: driver.close_window();

