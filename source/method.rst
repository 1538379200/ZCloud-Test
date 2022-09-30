=================
当前可用方法介绍
=================

进入网址
========

.. note::
	进入网址

.. py:function:: driver.get(url);

	:param url: 需要进入的网址
	:rtype: None


元素输入
=========

.. note::
	进行元素输入

.. py:function:: driver.send_keys(name, val, txt);

	:param name: 元素定位方式(xpath、id、name、css等)
	:param val: 元素值
	:param txt: 需要输入的数据


元素点击
=========

.. note::
	进行元素点击操作

.. py:function:: driver.click(name, val);

	:param name: 元素定位的方式
	:param val: 元素定位值


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


强制等待
=========

.. note::
	进行强制等待操作，单位为秒，程序将阻塞填入的时间长度

.. py:function:: driver.force_wait(timeout);

	:param timeout: 需要等待的时长，整数类型，单位秒


报告截图
=========

.. note::
	对浏览器进行元素截图或者全屏截图并存入报告，如果name或者val未填写，则默认进行全屏截图，否则为元素截图

.. py:function:: driver.report_shot(name, val);

	:param name: 选填，元素定位方式
	:param val: 选填，元素定位值


页面滚动
=========

.. note::
	进行页面滚动，此方法仅封装了滚动到底部和顶部的操作

.. py:function:: driver.scroll_top(top);
	
	:param top: 选填，布尔值，默认False，滚动到底部，为True时滚动到顶部


创建har
========

.. note:: 
	创建har，用于捕获网页network接口数据，使用此方法，必须启用了proxy代理

.. py:function:: driver.create_har();
	

获取network响应
================

.. note::
	获取网页中network的数据，并以列表的形式返回

.. py:function:: driver.get_har(filter_url);

	:param filter_url: 字符串类型，指定需要过滤的网址
	:rtype: 列表


切入iframe
============

.. note:: 
	切入到iframe的方法，如果val不填写，默认使用id、name的方式填入iframe，name则变成元素值

.. py:function:: driver.switch_iframe(name, val);

	:param name: 元素定位方式，当val为空时，name承担val职责
	:param val: 选填，元素定位值


切入最后一个句柄
================

.. note::
	默认切换到最后一个句柄，如果填写了参数，则以参数指定的句柄为准

.. py:function:: driver.switch_window_last(hint);

	:param hint: 选填，数字类型，选择当前的第几个句柄


获取元素属性
=============

.. note::
	定位元素并获取其属性值

.. py:function:: driver.get_attr(name, val, attr);
	
	:param name: 元素定位方式
	:param val: 元素定位值
	:param attr: 需要获取的属性名称

