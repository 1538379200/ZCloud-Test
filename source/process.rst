=====================
如何启用分布式多进程
=====================

用例标记
===========

在使用多进程的时候，我们需要使用 **@pytest.mark.user('admin', 'customer')** 这种形式的标记，来告诉程序，此用例需要分配给哪些账号使用，我们的多进程，是 **按照账号数量进行分配** 的


.. code-block:: python
 	:linenos:

 	@pytest.mark.user('admin', 'superagent', 'agent', 'customer')
	@pytest.mark.parametrize('data', [1, 2, 3, 4])
	def test_say_hello(data):
    	print(data, user)



用例过滤
===========

在很多时候，我们可能会直接在类上进行标记，来给类下所有的用例打上user标记，如果我们需要特定指定某一个用例过滤的话，就需要用到此标记

.. code-block:: python
	:linenos:

	@pytest.mark.user('admin', 'customer')
	class TestA:
	    def test_01(self):
	        print(1)
	     
	    def test_02(self):
	        print(2)
	     
	    @pytest.mark.ignore('customer')
	    def test_x(self):
	        print('x')


上述使用了ignore标记后，我们的admin进程，将运行所有用例，而customer，将不会运行test_x这个用例


运行启动多进程
================

上述的的操作，只是给我们的用例打上了标记，我们在运行的过程中，可以指定运行多少个账号和进程，以符合当前的运行期望

>>> pytest -n=4 --dist=each --users=admin,customer,superagent,agent --dynamic-log=True

.. warning::
	我们需要手动指定多少个进程，一个用户账号占据一个进程，--users指定了运行的账号，--dynamic-log对日志进行了处理，--dist=each则为每个进程分配同等的用例，我们可以使用程序的调试工具去进行，直接选择用户，程序将自动为其分配进程数量和日志模式


多进程的数据管理
==================

在我们的多进程中，使用多个账号进行，我们建议在数据模块中对测试的数据进行整理，而不是在用例逻辑中，当然，某些运行逻辑不相同的，你可能也是需要去进行一些逻辑修改的

在数据模块中判断当前运行用户，并指定账号运行的数据，你需要在运行前对模块进行重载（已不再需要重载）

在数据模块中，你可以使用confclass.worker来获取当前运行用户，用户有 **admin(运维)、general(总代)、agent(二级代理)、customer(客户)** 四种类型账号

进行数据模块重载（已优化，不需要重载）
----------------------------------------

对数据模块进行重载，你需要进入用例文件夹，比如：testcases/test_waf 文件夹，找到conftest.py文件，在里面导入你写好的数据模块，导入形式

.. code-block:: python
	
	import data.waf.data_equipment as waf_eq_data

然后，找到我们的reload_data函数，在其中，将这个waf_eq_data进行重载

.. code-block:: python
	:linenos:

	@pytest.fixture(scope='session', autouse=True)
	def reload_data():
    	importlib.reload(waf_eq_data)



