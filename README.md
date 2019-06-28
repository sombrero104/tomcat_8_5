https://tomcat.apache.org/download-80.cgi
http://mirror.apache-kr.org/tomcat/tomcat-8/v8.5.38/README.html

introduction
https://tomcat.apache.org/tomcat-8.5-doc/building.html#Introduction

ant 사용하기
https://mainia.tistory.com/1283

General > Editors > File Associations 에 .xml 추가.
Ant Editor를 디폴트로 사용하도록 설정.

svn 받기
https://svn.apache.org/repos/asf/tomcat/archive/tc8.5.x/tags
TOMCAT_8_5_38를 checkout.

---------------------------------------------------------------------------------------------------------------

Java > Build Path > Classpath Variables 설정 필요.

TOMCAT_LIBS_BASE :
The same location as the base.path setting in build.properties, where the binary dependencies have been downloaded
ANT_HOME :
the base path of Ant 1.9.8 or later

를 이렇게 설정.

TOMCAT_LIBS_BASE :
C:\[PROJECT HOME]\tomcat-build-libs
ANT_HOME :
C:\[STS HOME]\plugins\org.apache.ant_1.10.1.v20170504-0840

--
build.properties 파일의 base.path 경로 수정.

# base.path=${user.home}/tomcat-build-libs
base.path=C:/[PROJECT HOME]/tomcat-build-libs

---------------------------------------------------------------------------------------------------------------

https://svn.apache.org/repos/asf/tomcat/archive/tc8.5.x/tags/



build.xml
<property file="C:/[PROJECT HOME]/build.properties"/>
<srcfiles file="C:/[PROJECT HOME]/build.properties" />


---------------------------------------------------------------------------------------------------------------

https://stackoverflow.com/questions/5094786/eclipse-java-launch-configuration-file-path
launch 설정파일 경로
<workspace>/.metadata/.plugins/org.eclipse.debug.core/.launches
제공된 아래 파일을 편집해서 추가.
IDE 재시작하면 launch 설정에 Java Project로 새로 추가되어 있음.
/Tomcat_8_5_trunk/res/ide-support/eclipse/start-tomcat.launch
/Tomcat_8_5_trunk/res/ide-support/eclipse/stop-tomcat.launch


--
라이브러리가 일부만 다운로드 되어서 아래에서 가져와서 수정함. (버전 정보가 다름)
https://github.com/waihoyu/Apache-Tomcat-9/tree/master/TOMCAT_LIBS_BASE
--
다시 빌드하면 실행됨.
--
---------------------------------------------------------------------------------------------------------------

/bin/startup.sh -> /bin/catalina.sh start -> org.apache.catalina.startup.Bootstrap start

main(): daemon(catalinaDaemon -> org.apache.catalina.startup.Catalina)이 없을 경우 초기화(init() -> initClassLoaders() -> createClassLoader() 로 commonLoader, catalinaLoader, sharedLoader를 생성하여 각 라이브러리를 불러옴.)한 데몬을 저장한 Bootstrap을 만들고 daemon.load(args); 이후 데몬을 실행. daemon.start(); 

---------------------------------------------------------------------------------------------------------------



