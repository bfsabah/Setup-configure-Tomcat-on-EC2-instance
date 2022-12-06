# Setup-configure-Tomcat-on-EC2-instance

1- Create a RED HAT EC2 instance with standard configuration.

2- Connect to EC2 instance and switch to ROOT user : && sudo su

3- Install Java : && yum install java-1.8* {to check && java -version}

4- Download TOMCAT :    && mkdir opt

                        && cd opt

                        && wget {tomcat tar.gz file link}

                        && tar -xzvf {file name}
                    
5- Give Executing Permissin to startup.sh and shutdown.sh in /apache/bin :  && cd opt/apache/bin

                                                                            && chmod +x startup.sh

                                                                            && chmod +x shutdown.sh

6- We can startup or shutdown TOMCAT:   && ./startup.sh 


                                        && ./shutdown.sh

7- We can test TOMCAT: Copy your public IP address and paste it into your browser http://{public IP}:8080 #tomcat screen shows.

8- When we click "Manager App" Access Denied page is seen. To fix it we will find context.xml files and fix them.

    :   &&  find / -name context.xml {in webapps folders we have 2 context.xml files}

        && vim /opt/apache-tomcat-10.0.27/webapps/manager/META-INF/context.xml {we comment Valve Classname lines with <!-- --> }

        && ./shutdown.sh # restart Tomcat service

        && ./startup.sh

9- We refresh the page, now it asks for user credentials.

10 - We create a TOMCAT user:   && /opt/apache-tomcat-10.0.27/conf

                                &&  vim tomcat-users.xml

                                <role rolename="manager-gui"/>
 
                                <role rolename="manager-script"/>
                                <role rolename="manager-jmx"/>
                                <role rolename="manager-status"/>
                                <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
                                <user username="deployer" password="deployer" roles="manager-script"/>
                                <user username="tomcat" password="s3cret" roles="manager-gui"/>

                                paste these code block in tomcat-users.xml and save it. Restart TOMCAT service.

 11- Goto Tomcat Page and refrest, then login with "tomcat" account with password.

 12- Now you can use TOMCAT as your Webapp server. 