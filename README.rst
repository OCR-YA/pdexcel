df2xlsx
==========

An easy way to export DataFrame objects as tables and charts to excel file.

���㡢���ؽ�Pandas��DataFrame�����ΪExcel�ı��ͼ��,

һ���򵥵�����:

.. code-block:: python

   import numpy as np
   import pandas as pd
   from pd2xlsx import *
   
   dfa = pd.DataFrame(np.random.rand(14, 2), columns=list('AB'))
   dfb = pd.DataFrame(np.random.rand(10, 4), columns=list('ABCD'))

   # ����Excel�ļ�
   writer = ExcelWriter('demo2.xlsx')

   # ����������Sheet1
   sheet1 = writer.add_sheet(sheetname='Sheet1')
   # ��ӱ��1
   table11 = sheet1.add_table(dfa, table_name='Table_1')
   # ��ӱ��2, ��ֵ��ʽ�ٷֱ���λС�����п�����Ϊ8.
   table12 = sheet1.add_table(dfb, dicformat={'num_format':'0.00%'}, width=6)
   # ����ͼ��, Ĭ��Ϊ����ͼ
   chart11 = table11.add_chart()
   # ����ֱ��ͼ, ����'Column Chart'
   chart12 = table12.add_chart(chart_name='Column Chart', chart_type='column')
   # ���� A��C�������ݵ�����ͼ, �߶�ΪĬ�ϵ�2��
   chart13 = table12.add_chart(chart_col=['A','C'], y_scale=2)
   
   # ����������Sheet2
   sheet2 = writer.add_sheet()
   # ����ָ�����ı��
   table2 = sheet2.add_table(dfa, tbl_style='Table Style Light 11')
   # ����ָ������ͼ��
   chart2 = table2.add_chart(chart_style=37)
   
   # �˳��������ļ�
   writer.close()

.. image:: https://raw.github.com/UncleJiong/pdexcel/master/example/demo1a.png

.. image:: https://raw.github.com/UncleJiong/pdexcel/master/example/demo1b.png

Ҳ����ͨ��`to_excel`��������������Excel�ļ�:

.. code-block:: python

   import numpy as np
   import pandas as pd
   from pd2xlsx import *
   
   dfa = pd.DataFrame(np.random.rand(14, 2), columns=list('AB'))
   dfb = pd.DataFrame(np.random.rand(10, 4), columns=list('ABCD'))

   with ExcelWriter('demo.xlsx') as writer2:
       # ������Sheet1, ��A��C�ֶ����ݻ�����ͼ
       sheet1 = to_excel(writer2, dfa, kwargs_chart=dict(chart_col=['A', 'C']))
       # ������Sheet1, ����ͼ, ��ֵ�԰ٷֱȸ�ʽ����
       sheet1 = to_excel(writer2, dfb, sheet1, chart=False,
                         kwargs_cell={'num_format':'0.00%'})
       # ������Sheet2, ��ֱ��ͼ
       sheet2 = to_excel(writer2, dfa, chart_type='column')
	   

.. image:: https://raw.github.com/UncleJiong/pdexcel/master/example/demo2a.png

.. image:: https://raw.github.com/UncleJiong/pdexcel/master/example/demo2b.png