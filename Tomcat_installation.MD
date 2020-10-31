1) sudo yum install epel-release
2) sudo yum update -y && sudo reboot
3) sudo yum install java-1.8.0-openjdk.x86_64
4) java -version
5) sudo groupadd tomcat
6) sudo mkdir /opt/tomcat
7) sudo useradd -s /bin/nologin -g tomcat -d /opt/tomcat tomcat
8) cd ~
9) wget http:"http from tomcat web-site"
10) sudo tar -zxvf apache-tomcat-8.*.tar.gz -C /opt/tomcat --strip-components=1
11) cd /opt/tomcat
12) sudo chgrp -R tomcat conf
13) sudo chmod g+rwx conf
14) sudo chmod g+r conf/*
15) sudo chown -R tomcat logs/ temp/ webapps/ work/
16) sudo chgrp -R tomcat bin
17) sudo chgrp -R tomcat lib
18) sudo chmod g+rwx bin
19) sudo chmod g+r bin/*
20) sudo vi /etc/systemd/system/tomcat.service
21) type into tomcat.service

========================================================================

[Unit]
Description=Apache Tomcat Web Application Container
After=syslog.target network.target

[Service]
Type=forking

Environment=JAVA_HOME=/usr/lib/jvm/jre
Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid
Environment=CATALINA_HOME=/opt/tomcat
Environment=CATALINA_BASE=/opt/tomcat
Environment='CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC'
Environment='JAVA_OPTS=-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom'

ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/bin/kill -15 $MAINPID

User=tomcat
Group=tomcat

[Install]
WantedBy=multi-user.target

========================================================================

22) sudo yum install haveged (for a security-related program)
23) sudo systemctl start haveged.service
24) sudo systemctl enable haveged.service
25) sudo systemctl start tomcat.service
26) sudo systemctl enable tomcat.service
27) sudo firewall-cmd --zone=public --permanent --add-port=8080/tcp
28) sudo firewall-cmd --reload
29) http://[your-server-IP]:8080
30) sudo vim /opt/tomcat/conf/tomcat-users.xml
31) type into to last column tomcat-users.xml

========================================================================
<role rolename="manager-gui"/>
 <role rolename="manager-script"/>
 <role rolename="manager-jmx"/>
 <role rolename="manager-status"/>
 <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
 <user username="deployer" password="deployer" roles="manager-script"/>
 <user username="tomcat" password="s3cret" roles="manager-gui"/>

========================================================================

32) sudo systemctl restart tomcat.service
33) find / -name context.html
34) vim /opt/tomcat/webapps/host-manager/META-INF/context.xml

========================================================================

<!--  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
               allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->
               
type <!-- --> in front of Valve column.Not only local adress also you can access global web.               

========================================================================

35) vim /opt/tomcat/webapps/manager/META-INF/context.xml  (repar 34)
36) Artiq hem local vm den hemde globaldan cixish olacaqdir tomcata.
