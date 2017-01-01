<h2><b>MongoDB学习-函数和游标</b></h2>
<p>在<a href="https://www.oracle.com/index.html">Oracle</a>、<a href="http://www.mysql.com/">Mysql</a>、<a href="https://www.mongodb.com/">MongoDB</a>中，只要接触过procedure,就应该知道游标和聚合函数，接下来讲解一些简单常用的聚合函数</p>
<p>一：聚合函数</p>
<p>① count</p>
<p>用来计数，可以传入JSON对象作为条件。</p>
<img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb_count_1.png" />
<p>② distinct</p>
<p>distinct和其他数据库效果一样，用于去重。</p>
<img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb_distinct_1.png"/>
<p>③ group</p>
<p>group的效果是分组，但操作上比较复杂。你可以把它看出js一个函数，传入指定参数，实现方法</p>
<ul>
  <li>key:指分组的字段</li>
  <li>initial:初始化函数</li>
  <li>reduce:该函数有两个参数，第一个指当前文档对象，第二个指function操作累计对象。初始化对象有多少个，reduce函数就会调多少次</li>
  <li>finalize:每一组文档完成后触发</li>
  <li>condition:分组过滤条件</li>
</ul>
<img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb_group_1.png"/>
<p>④ mapReduce</p>
<p>mapReduce严格来说用于map分组后的简化，比group复杂多，灵活性强,主要围绕map和reduce来操作数据</p>
<p>map: 映射函数，主要调用emit(key,value),集合会根据key进行分组</p>
<p>reduce:简化函数，会对map分组后的数据进行分组简化，注意：在reduce(key,value)中的key就是emit中的key，vlaue为emit分组后的emit(value)的集合，这里也就是很多{"count":1}的数组。</p>
<p>mapReduce:这个就是最后执行的函数了，参数为map，reduce和一些可选参数</p>
<img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb_mapReduce_1.png"/>
<p>从图中我们可以看到如下信息：</p>
<ul>
  <li>result: "存放的集合名“。</li>
  <li>input:传入文档的个数。</li>
  <li>emit：此函数被调用的次数。</li>
  <li>reduce：此函数被调用的次数。</li>
  <li>output:最后返回文档的个数.</li>
</ul>
<p>分组后生成的集合：</p>
<img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb_mapReduce_2.png"/>

<p>二：游标</p>
<p>Oracle的存储过程中，游标往往用于遍历数据集，进行相关操作。mongodb的原理也一样，根据find()获取一个JSON对象数组，遍历数组里面的JSON对象进行相关操作。稍微灵活点就是取出对象进行链式操作，和jq一样</p>
<img src ="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongdb_cursor_1.png"/>
