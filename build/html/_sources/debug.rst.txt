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
	当我们给用例添加了story、feature等标志后，我们可以根据这个来确定用例的运行，具体可以使用哪些方法，可以通过pytest --help或者pytest -h来查看，查看关于allure的命令行参数，windows查看仅关于allure的参数可以 **pytest --help | findstr allure** 


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


测试失败终止代码
==================

.. note:: 
	在pytest运行中，用例失败不会停止代码，如果我们在调试代码的时候，则可以让其运行失败的时候，直接停止，方便我们直接进行调试操作

.. code-block:: python
	:linenos: 

	# 加上-x，则代码运行到失败会终止运行
	pytest.main(['-x'])


运行上次失败的用例
====================

.. note::
	pytest在运行后，会保存各个用例的状态，保存在我们项目目录的 **.pytest_cache** 目录，我们可以使用命令行参数，使pytest仅运行上次失败的用例

.. code-block:: python
	:linenos:

	# 运行失败的用例
	pytest.main(['--lf'])	# pytest.main(['--last-failed'])

	# 先运行失败的用例再运行其他用例
	pytest.main(['--ff'])	# pytest.main(['--failed-first'])

	# 我们可以手动清除上次的运行缓存，但是一般不需要去手动清理
	pytest.main(['--cache-clear'])


步进调试
============

.. note:: 
	调试失败用例，我们还可以使用步进的方式，和-x参数一样，遇到失败会停止运行，下次再以此模式运行，将从这个失败的用例继续运行

.. code-block:: python
	:linenos:

	pytest.main(['--sw'])

	# 我们还可以使用 --stepwise-skip 的方式跳过第一个失败的用例，即从上次失败的下一个用例开始
	pytest.main(['--sw', '--stepwise-skip'])


