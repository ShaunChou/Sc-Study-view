<h3>MongoDB学习-安装配置</h3>
  <h5><p>&nbsp;&nbsp;&nbsp;&nbsp;本人第一次接触MongoDB,他比Oracle、Mysql、Sql server更好操作。唯一缺点是原本不支持事务、多表联查<p>

    <p>一：下载</p><p> &nbsp;&nbsp;上<a href="http://www.mongodb.org/downloads">MongoDB官网</a>根据不同的系统选择，<u style="color :red">特别注意两点:</u>
            <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;①：根据业界规则，偶数为“稳定版”，奇数为“开发版”
            <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;②：32bit的mongodb最大只能存放2G的数据，64bit就没有限制。</p></p>
  </p>本人系统是OSX,所以下面安装指令是OSX为主,只供参考：</p>
</p><p>二：启动</p>
              <p>&nbsp;&nbsp;①：解压下载tgz文件，然后通过cp指令复制到你指令的文件夹。当然可以不使用指令copy也行</p>
              <p>&nbsp;&nbsp;②：通过vim生成一个配置文件</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;然后执行下面指令：</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sudo chown -R root mongodb.config</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sudo ./mongod -f mongodb.config</p>
              <p>&nbsp;&nbsp;③:如何把Mongodb服务设置为开机启动项</p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;创建一个mongodb.plist文件，把文件移动到~/Library/LaunchDaemons
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;执行指令：sudo chown -R root  /Library/LaunchDaemons/mongod.plist </p>
              <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sudo launchctl load /Library/LaunchDaemons/mongod.plist  </p>
  </p>
</h5>
