<h2><b>MongoDB学习-索引操作</b></h2>
<p>数据库中，往往会遇到查询数据，响应时间超长的问题，那我们如何对程序性能进行优化了。</p>
<p>首先可能想到的就是索引，下面主要介绍索引的简单操作。version：3.4.1</p>
<p>一：性能分析函数（explain）</p>
<p>用于获取查询请求返回的统计数据，同时可以针对性的优化索引</p>
<img src="https://github.com/ShaunChou/Sc-Study-view/blob/master/imag/MongoDB/mongodb_index_1.jpg" alt="explain">
<p>nReturned:返回的条数</p>
<p>executionTimeMillis:执行需要的时间(毫秒)</p>
<p>totalDocsExamined:总的条数</p>
<p>二：优化器profile</p>
<p>① 开启profiling功能</p>
<p>有两种方式可以控制 Profiling 的开关和级别，第一种是直接在启动参数里直接进行设置。</p>
  </p>启动MongoDB 时加上–profile=级别 即可。也可以在客户端调用db.setProfilingLevel(级别) 命令来实时配置，Profiler 信息保存在system.profile 中。</p>
<p>我们可以通过db.getProfilingLevel()命令来获取当前的Profile 级别，类似如下操作：</p>
<p>db.setProfilingLevel( level , slowms )，第一个参数是级别，第二个是时间</p>
<p>级别主要有三种分别是</p>
<ul>
  <li>0 – 不开启</li>
  <li>1 – 记录慢命令 (默认为>100ms)</li>
  <li>2 – 记录所有命令</li>
</ul>
<p>② 查询 Profiling 记录</p>
<p>例如：查询执行时间大于5条的数据</p>
<p>db.system.profile.find( { millis : { $gt : 5 } } )</p>
<p>查询最新的一条记录</p>
<p>db.system.profile.find().sort({$natural:-1}).limit(1)</p>
<p>三：性能监控工具</p>
<p>这个不做过多的描述，感兴趣的可以参考官网文档</p>
<ul>
  <li>1. mongosniff</li>
  <li>2. Mongostat</li>
  <li>3. db.serverStatus</li>
  <li>4. db.stats</li>
</ul>
<p>接下来就开始正式讲索引的操作</p>
<p>四：索引</p>
<p>1.基础索引</p>
<p>在字段age 上创建索引，1(升序);-1(降序)：</p>
<p>db.users.ensureIndex({age:1})</p>
<p>_id 是创建表的时候自动创建的索引，此索引是不能够删除的。当系统已有大量数据时，创建索引就是个非常耗时的活，</p>
<p>我们可以在后台执行，只需指定“backgroud:true”即可。</P>
<p>db.users.ensureIndex({age:1} , {backgroud:true})</p>
<p>2.文档索引</p>
<p>索引可以任何类型,甚至文档：</p>
<p>db.factories.insert( { name: "wwl", addr: { city: "Beijing", state: "BJ" } } );</p>
<p>//在addr 列上创建索引</p>
<p>db.factories.ensureIndex( { addr : 1 } );</p>
<p>//下面这个查询将会用到我们刚刚建立的索引</p>
<p>db.factories.find( { addr: { city: "Beijing", state: "BJ" } } );</p>
<p>//但是下面这个查询将不会用到索引，因为查询的顺序跟索引建立的顺序不一样</p>
<p>db.factories.find( { addr: { state: "BJ" , city: "Beijing"} } );</p>
<p>3.组合索引</p>
<p>跟其它数据库产品一样，MongoDB 也是有组合索引的，下面我们将在addr.city 和addr.state上建立组合索引。当创</p>
<p>建组合索引时，字段后面的1 表示升序，-1 表示降序，是用1 还是用-1 主要是跟排序的时候或指定范围内查询 的时</p>
<p>候有关的。另外,升序和降序的顺序不同都会产生不同的索引</p>
<p>db.factories.ensureIndex( { "addr.city" : 1, "addr.state" : 1 } );</p>
<p style="color : red">注：只要查找的条件字段在索引中有，顺序最好与索引中一致，但如果索引中的第一个字段没有出现在条件中，则不会用索引</p>
<p>4. 唯一索引</p>
<p>创建</p>
<p>db.t4.ensureIndex({firstname: 1, lastname: 1}, {unique: true});</p>
<p>删除唯一索引</p>
<p>db.test.dropIndex({"userid":1})</p>
<p>创建唯一索引,并消除重复数据</p>
<p>db.users.ensureIndex({"age":1},{"unique":true,"dropDups":true})</p>
<p>创建组合唯一索引</p>
<p>db.users.ensureIndex({"name":1,"age":1},{"unique":true})</p>
<p style="color : red">注：insert的时候要注意主键重复，没有插入组件的问题</p>
<p>5.强制使用索引</p>
<p>db.users.find({age:{$lt:30}}).hint({name:1, age:1}).explain()</p>
<p>6.删除索引</p>
<p>db.t3.dropIndexes()</p>
<p>db.t4.dropIndex({firstname: 1})</p>
<p>db.t4.dropIndexes("索引名") </p>
<p>db.t4.dropIndex(‘*’)   _id索引不会删除</p>
<p>7 地理空间索引</p>
<p>db.shopstreet.ensureIndex({"gps" : "2d"},{"min":-1000,"max":1000});  </p>
<p>8 复合地理空间索引</p>
<p>db.showstreet.ensureIndex({"gps":"2d", "desc":1});  </p>
<p>9 Sparse索引（稀疏索引）</p>
<p>db.Mail.ensureIndex({labels:1},{sparse:true})</p>
<p>10 Covered 索引（覆盖索引）</p>
<p>如果你查找的值正好是在索引中，则可以直接返回索引中存的值，而不用到数据文件中查找。（这个在传统关系型</p>
<p>数据库中也有实现），不过，必须满足以下条件：</p>
<p>Ø 必须提供准备的返回字段，以便可以直接从索引库中查询</p>
<p>Ø 必须明确地排除使用_id字段{_id：0}</p>
<p>即返回的字段就在索引中</p>
<p>当用explain时，当indexOnly=true，表示有用到covered index:</p>
<p>11 查看索引</p>
<p>getindexes可以查看索引，db.集合名.getindexes()</p>
<p>12 正则表达式在索引中的使用</p>
<p>13 索引分析</p>
<p>14 为排序创建索引</p>
<hr>
<p>性能优化方案<p>
<ul>
  <li>创建索引</li>
  <li>限定返回结果数</li>
  <li>只查询使用到的字段</li>
  <li>采用capped collection</li>
  <li>采用Server Side Code Execution</li>
  <li>使用Hint，强制使用索引</li>
  <li>采用Profiling</li>
  <li>尽量少用低效率的操作符 $exists,$ne,$not,$nin</li>
  <li>复合索引中一般精确匹配的放前面，范围的放后面</li>
  <li>$or可以对每个字句使用索引，因为$or实际是执行多次查询再合并结果</li>
</ul>
