=========================
框架中众多装饰器的作用
=========================


自定义标记模块
===============

.. note:: 
	我们有三个自定义的mark标记，control、waf、monitor，用于标记不同的模块，通过模块间的解耦，让运行更加灵活

.. code-block:: python
	:linenos:

	@pytest.mark.control
	def test():
		...

	@pytest.mark.waf
	def test():
		...

	@pytest.mark.monitor
	def test():
		...


allure的报告标记
=================

.. note::
	allure的标记是属于pytest-allure的插件装饰器，用于给allure提供数据的

.. code-block:: python
	:linenos:

	@allure.epic('xxx')		# 标记测试的系统
	@allure.feature('xxx')	# 标记测试的模块
	@allure.story('xxx')	# 标记用例功能，故事级
	@allure.title('xxx')	# 标记用例名称
	@allure.step('xxx')		# 标记用例步骤
	def test():
		...


确立用例之间依赖
=================

.. note::
	我们的用例之间，很多时候是存在依赖关系的，比如，只有A用例成功过后，我们才会想要运行B用例，B依赖于A的结果，这个时候，我们可以使用dependency插件装饰器来确立依赖关系

.. code-block:: python
	:linenos:

	@pytest.mark.dependency(name='case')
	def test_001_xxx():
		...

	@pytest.mark.dependency(depends=['case'])
	def test_002_xxx():
		...


.. tip::
	我们上面案例，当test_001_xxx运行失败的时候，test_002_xxx将会自动跳过，dependency默认的范围是module，按照当前文件，这个可以自行去搜索相关使用方法，建议每个被依赖的方法、函数，都应该使用唯一的name标识


用例参数化
============

.. note::
	用例参数化，可以让我们使用当前的方法，仅修改参数，来达到产生不同用例的目的，下面会产生两个用例，形参xxx将会被两个实参yyy和zzz取代

.. code-block:: python
	:linenos:

	@pytest.mark.parametrize('xxx', ['yyy', 'zzz'])
	def test(xxx):
		...



跳过用例
==========

.. code-block:: python
	:linenos:

	@pytest.mark.skip()
	def test():
		...

	@pytest.mark.skipif(xxx)
	def test():
		...


确认用例执行顺序
=================

.. note::
	确认用例顺序会作用于全局，建议不使用这种方式，而是采取名称的方式来确定运行顺序

.. code-block:: python
	:linenos:

	@pytest.mark.run(order=1)
	def test():
		...


预期失败
==========

.. note:: 
	在某些场景下，我们的用例，在预想情况下就应该是失败的，这时候可以使用xfail的预期失败，当用例失败，标记为 **xfail** 表示是预期内的失败，如果通过了，则标记为 **xPass** 表示为预期外的通过，xfail并不算做失败用例

.. py:function:: @pytest.mark.xfail(condition=None, reason=None, raises=None, run=True, strict=False);
	
	:param condition: 条件，满足某些条件执行预期结果，condition返回True为执行
	:param reason: 原因，可以进行一些描述
	:param raises: 指定一些错误情况，错误之外的错误，则会标记用例为fail，而不是xfail
	:param run: 如果为False，则不运行用例，直接标记为xfail
	:param strict: 当为False时，失败标记为xfail，成功标记为xpass；如果为True，用例通过则直接标记为fail


跳过整个class
===============

.. note:: 
	这是我们自己定义的mark标记，源码在项目根目录的conftest.py文件中，使用此标记，可以根据用例运行状态，跳过整个class的运行，具体实现逻辑，当用例被标记上过后，如果此用例运行失败，则会计算重试最大次数，达到最大重试次数后仍是失败，则会记录此class或者此module，其他属于被记录的class或者module的用例将会被跳过运行

.. py:function:: @pytest.mark.skipclass(module);
	
	:param module: 布尔值，此参数必须使用关键词的形式，当为True时，跳过整个文件的用例，False或者默认跳过当前class

.. code-block:: python
	:linenos:

	@pytest.mark.skipclass	# 当用例运行状态不是passed时，跳过此class后面即将运行的所有用例
	def test_001():
		...

	@pytest.mark.skipclass(module=True)	# 如果用例状态不是passed时，跳过整个文件运行
	def test_003():
		...

