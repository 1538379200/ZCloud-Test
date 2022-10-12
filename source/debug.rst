======================
如何自定义运行、调试
======================


运行时选择用例
==================

.. note:: 
	在代码编写过程中，我们编写的用例可能不需要单独进行调试，运行全部用例可能会拖延我们的运行时间，我们可以指定需要运行的文件或者用例

.. code-block:: python
	:linenos:

	pytest.main(['testcases/test_001_xxx.py::Test002XXX::test_000_xxx'])


.. note:: 
	上面代码，指定了运行用例 **test_000_xxx** ，前面testcases是文件夹，test_001_xxx.py是用例保存文件，Test002XXX是用例类名，前面定位到文件，使用的是 ”/“ 后面指定类和方法，使用的是 ”::“ ，我们可以指定多个，也可以单独只指定类名或者文件，目录按这行代码的相对路径找（一般为main.py文件）



使用pytest跳过用例
====================

.. note::
	有些时候，当我们需要运行多条用例调试，当我们用例并不是很多的时候，可以给不想运行的用例打上skip，来跳过这个用例的执行

.. code-block:: python
	:linenos:

	@pytest.mark.skip
	def test_000_xxx(self, driver):
		print("跳过用例")


使用allure来确定运行的用例
============================

.. note:: 
	当我们给用例添加了story、feature等标志后，我们可以根据这个来确定用例的运行，具体可以使用哪些方法，可以通过pytest --help来查看，查看关于allure的命令行参数，windows查看仅关于allure的参数可以 **pytest --help | findstr allure** 


.. code-block:: python
	:linenos:

	@allure.story("测试")
	@allure.severity('blocker')
	class Test:
		def test_001_xxx(self, driver):
			print("都跳过运行")

	# 根据story进行划定
	pytest.main(['--allure-stories=测试'])

	# 根据设置的优先级进行划定
	pytest.main(['--allure-severities=blocker'])

