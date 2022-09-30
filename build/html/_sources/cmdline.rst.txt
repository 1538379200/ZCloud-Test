=======================
命令行自定义参数介绍
=======================


开启代理模式
=============

.. note::
	当我们需要获取network中的返回时，需要启动我们的代理服务，开启代理服务过后，我们的获取方法才能生效

.. code-block:: python
	:linenos:
	:emphasize-lines: 2

	# 必须写上值，为True则启动服务
	pytest.main(['--useproxy=True'])


>>> pytest --useproxy=True


开启动态日志名称
================

.. note::
	当我们在使用多进程的时候，多进程的运行会覆盖日志文件，在使用多进程的时候，建议开启此选项，使用uuid自定义文件名称，防止日志文件覆盖，另外，每次项目运行，都会执行一遍清空日志文件夹的操作

.. code-block:: python
	:linenos:
	:emphasize-lines: 2

	# 必须写上值
	pytest.main(['--dynamic-log=True'])

>>> pytest --dynamic-log=True


切换测试环境
==============

.. warning::
	目前此功能暂未开发完成，等待后续数据补足后在进行维护

.. code-block:: python
	:linenos:
	:emphasize-lines: 2

	# 必须写上值，目前未确定值
	pytest.main(['--env=xxx'])

>>> pytest --env=xxx
