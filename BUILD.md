- download spark source code
```
$ wget -c http://mirrors.tuna.tsinghua.edu.cn/apache/spark/spark-2.3.1/spark-2.3.1.tgz
$ tar -xzf spark-2.3.1.tgz
$ cd spark-2.3.1
```

- install jdk1.8 and apache-maven-3.3.9 or newer

- vim pom.xml
```
  <repositories>
    <repository>
      <id>central</id>
      <!-- This should be at top, it makes maven try the central repo first and then others and hence faster dep resolution -->
      <name>Maven Repository</name>
      <url>http://maven.aliyun.com/nexus/content/repositories/central/</url>
      <releases>
        <enabled>true</enabled>
      </releases>
      <snapshots>
        <enabled>false</enabled>
      </snapshots>
    </repository>
    <repository>
      <id>cloudera</id>
      <name>cloudera repository</name>
      <url>https://repository.cloudera.com/artifactory/cloudera-repos/</url>
    </repository>
  </repositories>
  <pluginRepositories>
    <pluginRepository>
      <id>central</id>
      <url>http://maven.aliyun.com/nexus/content/repositories/central/</url>
      <releases>
        <enabled>true</enabled>
      </releases>
      <snapshots>
        <enabled>false</enabled>
      </snapshots>
    </pluginRepository>
  </pluginRepositories>
```

- build
```
$ export MAVEN_OPTS="-Xmx2g -XX:ReservedCodeCacheSize=512m"
$ cd spark-2.3.1; ./dev/make-distribution.sh --name 2.3.1-chd5.10.0 --tgz --mvn /opt/apache-maven-3.3.9/bin/mvn -Pyarn -Phadoop-2.6 -Phive-thriftserver -Phive -Pnetlib-lgpl -Dhadoop.version=2.6.0-cdh5.10.0 -DskipTests -Dproject.version=2.3.1
```
