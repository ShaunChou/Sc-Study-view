<h2><b>MongoDB学习-增删改查</b></h2>
<p>MongoDB学习从现在正式开始，它虽然没有Oracle强大，但在处理某些日志和临时信息的保存下，又有很大的优势</p>
<p>首先介绍一款可视化工具<a href="http://www.toadworld.com/products/toad-for-oracle">Toad</a>,可用于<a href="https://www.oracle.com/index.html">Oracle</a>、<a href="http://www.mysql.com/">Mysql</a>、<a href="https://www.mongodb.com/">MongoDB</a>。</p>
<p>一：Insert操作</p>
   <p>MongoDB操作方式和其他数据库不一样，主要的数据是JSON对象，如果对JSON了解，学习是手到擒来</p>
   <p>常见的插入有两种形式：“单行插入”、“批量插入”</p>
   <p>① 单行插入</p>
   <img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb_insert_1.png"/>
   <p>② 多行插入</p>
   <img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb_insert_2.png"/>
<p>在学下面三种操作前，先熟悉一下Mongdb封装的指令</p>
<ul>
    <li><a href="#"title="大于">$gt</a></li>
    <li><a href="#"title="大于等于">$gte</a></li>
    <li><a href="#"title="小于">$lt</a></li>
    <li><a href="#"title="小于等于">$lte</a></li>
    <li><a href="#"title="不等于">$ne</a></li>
    <li><a href="#"title="或">$or</a></li>
    <li><a href="#"title="在...之内">$in</a></li>
    <li><a href="#"title="不在...之内">$nin</a></li>
    <li><a href="#"title="在哪里">$where</a></li>
    <li><a href="#"title="在原基础上操作，常用于递增操作">$inc</a></li>
    <li><a href="#"title="改变值">$set</a></li>
</ul>
<p>二：Delete操作</p>
  <p>MongoDB数据库没用到DELETE做删除关键字，而是用Remove，这也更好的形容JSON对象操作</p>
  <img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb_remove_1.png"/>
  <p>上面只是简单的操作，你也可以根据不同的条件进行多行删除。</p>
<p>三：Update操作</p>
  <p>① $inc使用<p>
  <p>如果大学接触过微软sql server的同学，应该对$inc不会陌生，每次修改在原有的基础上自增，例如sql server中创建自增长的主键</p>
  <img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb.update_1.png"/>
  <p>② $set使用</p>
  <p>会一点后台语言对set应该不陌生,set就等于给对象赋值的方法</p>
  <img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb.update_2.png"/>
  <p>③ 整体更新</p>
  <p>整体更新主要是根据条件，把要更新的值放到一个JSON对象里面</p>
  <img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb_update_3.png"/>
  <ul>
    <li>局部更新</li>
    <ol type="1">
      <li>第一个query是必填项，如果没有设置条件执行就会报错</li>
      <li>第二个条件update对象。如果对象key不存在，就会增加一个key。在开发的时候学会尽量避免写错key导致生成新字段的问题。<sup style="color :red">*</sup></li>
      <li>第三个参数为true，query条件找不到数据，会自动生成一条新数据。<sup style="color :red">*</sup></li>
      <li>第四个参数为true，query条件匹配多条，会批量更新多条记录，否则只更新一条</li>
    </ol>
    <li>整体更新</li>
     <ol type="1">
     <li>第一个query是必填项，如果没有设置条件执行就会报错</li>
     <li>第二个条件update对象。如果对象key不存在，就会增加一个key。在开发的时候学会尽量避免写错key导致生成新字段的问题。<sup style="color :red">*</sup></li>
     <li>第三个参数为true，query条件找不到数据，会自动生成一条新数据。<sup style="color :red">*</sup></li>
     <li>整体更新只有三个参数，只能更新一条记录，不可以批量更新。</li>
     </ol>
  </ul>
<p>四：Select操作</p>
   <p>Select相对来说很简单，和Delete操作一样。但玩法很多，对于喜欢js的我，非常棒</p>
    <img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb.select_1.png"/>
