======================
进行postgresql的读取
======================


简介
=========

框架使用的核心数据库是postgresql，用于存储用例，便于后续的管理和发展，目前数据库的数据存储尚在考虑阶段，因为其存入形式目前并不友好，但是我们的读取已经提供了一些方法了，使用此方法需要导入类，方法主要依赖查询当前的用例，我们的存储也是按步骤进行存储，所以一个用例也查询出来多个步骤

.. code-block:: python
	:linenos:

	from config.pgsql import GetSql

	s = GetSql('表', '用例名称')		# 后面我们统一用s代替GetSql的实例


我们还可以使用with的形式去进行，程序会自动进行数据库的关闭操作

.. code-block:: python
	:linenos:

	from config.pgsql import GetSql

	with GetSql('表', '用例名称') as s:
		print(s.all)


获取所有数据
=============

.. note:: 
	all方法将返回关于用例的所有数据

.. py:function:: s.all;
	
	:rtype: list




获取所有步骤名称
=================

.. note::
	steps将返回所有步骤的名称，列表形式

.. py:function:: s.steps;

	:rtype: list


获取所有的步骤值
==================

.. note::
	我们存储时，一个字段代表一个值，所以我们存储的定位方式和元素值是分开的，使用values可以取出所有的值，以列表形式返回，定位方式和元素值会以元组方式集合在一起

.. py:function:: s.values;
	
	:rtype: list[tuple]


获取单个步骤
=============

.. note:: 
	当我们只想获取一个步骤的时候，我们可以使用此方式，此方式是重新进行sql查询，获取单个步骤的所有值

.. py:function:: s.get_step(step_name, value_only);

	:param step_name: 步骤名称
	:param value_only: 布尔值，默认True，只会返回一个包含定位方式和定位值的元组，为False则返回所有数据的元素


以字典方式返回步骤值
====================

.. note::
	我们的实际使用的过程中，可能单纯的元组，不好去确定值，我们可以使用此方式，将数据作为一个字典出现，然后我们可以通过步骤的值去进行筛选操作，值的形式为： **{'步骤名': ('xpath', '//div[@id="su"]')}** 

.. py:function:: s.dict_step;
	
	:rtype: dict



关闭数据库连接
===============

.. py:function:: s.close();



便捷添加数据
==============

添加数据我们可以运行框架根目录的 **insert_cases.py** 文件，cd到根目录运行命令：
``streamlit run insert_cases.py``

使用此方式需要安装必要的依赖： streamlit, pandas, psycopg2

.. image:: images/index.png

