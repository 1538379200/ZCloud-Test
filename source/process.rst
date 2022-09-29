=====================
如何启用分布式多进程
=====================

在运行的时候，我们可以指定需要启动多少个进程，一个进程调用一个CPU资源

>>> pytest -n=2 --dist=loadscope


在py文件中写入即是

.. code-block:: python
	:linenos:

	pytest.main(['-n=2', '--dist=loadscope'])



.. note::
	使用分布式多进程时，-n是指定几个进程，根据设备配置来，--dist可以使用参数load、loadfile、loadscope、no、each，几种，loadfile是一句py文件进行分组，loadscope是依据module和class进行分组，以class为准，each是线程运行所有的用例



