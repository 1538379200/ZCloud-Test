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

.. note:: 
	进行测试环境切换，切换环境需要保证新的配置数据结构与 **preconditions.ini** 的结构相同，只是数据值进行不同的变更，不填写此参数，默认为读取 **preconditions.ini** 文件


.. code-block:: python
	:linenos:
	:emphasize-lines: 2

	# 必须写上值，如果值不是 test 则会认为是正式环境，启用其他文件
	pytest.main(['--env=xxx'])

>>> pytest --env=xxx

.. warning::
	每个环境应该拥有一份自己的配置文件，他们可能在数据层面有所不同，但都具有相同的结构， **preconditions.ini** 为测试环境配置数据，目前暂定 **preconditions_pro.ini** 为正式环境配置文件名，具体读取哪份文件，可以在项目根目录的 **conftest.py** 文件中，找到钩子函数 **pytest_configure** 修改其文件路径


使用selenium无头模式运行
===========================

.. note:: 
	默认不使用无头模式运行，只有值为True才启动无头模式

.. code-block:: python
	:linenos:

	# 仅在值等于True的时候，开启无头模式
	pytest.main(['--headless=True'])