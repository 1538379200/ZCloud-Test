========================
设置用例的优先级
========================


优先级分类
============

.. note:: 
	在用例标记时，我们会将用例按照业务功能，进行优先级划分，可以分为 [BLOCKER]_, [CRITICAL]_, [NORMAL]_, [MINOR]_, [TRIVIAL]_ 在zcloud自动化中，给定优先级，会在报告中进行体现，很容易查看到各种优先级的运行通过情况
	allure使用的默认优先级为normal



.. [BLOCKER] 严重阻塞，不能进行下一步

.. [CRITICAL] 严重缺陷，功能点缺失等

.. [NORMAL] 一般缺陷

.. [MINOR] 次要缺陷，可能页面与设计不符合等

.. [TRIVIAL] 轻微缺陷，基本为可优化



代码中标记优先级
==================

.. note:: 
	在代码中标记优先级，需要导入allure模块，然后进行优先级设置


.. code-block:: python
	:linenos:

	@allure.severity(allure.severity_level.BLOCKER)
	def test_demo():
		xxx

	# 也可以使用字符串的形式，不区分大小写
	@allure.severity('BLOCKER')
	def test_demo():
		xxx


指定运行特定优先级用例
=======================

.. code-block:: python
	:linenos:

	# 仅运行block和normal优先级的用例
	pytest.main(['--allure-severities=blocker, normal'])

	# 设置了story、featur等，也可以根据story进行运行划分,详细使用 pytest --help 查看
	pytest.main(['--allure-stories=story1, story2'])

	pytest.main(['--allure-features=feature1, feature2'])


