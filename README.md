Allow deploy command to accept URI
=====================

Implementing http://java.net/jira/browse/GLASSFISH-12699

## Design Documentation 
Pl. see the deployuri one pager I have attached to the root directory.

## Building
Step1. Update the GF project to the latest version and build it.

Step2. Copy the changes as written in RemoteRestAdminCommand.patch to the RemoteRestAdminCommand.java and build this comp.(common-util.jar)

Step3. copy the DeployUriCommand.java to the directory of nuclear\deployment\admin\src\main\java\org\glassfish\deployment\admin and build the deployment-admin module
and build this comp(deployment-admin.jar)
Step4. access to the directory of appserv\packager\external\apache-commons-net and build it to install the common-net.jar into osgi bundles. 

##Deployuri command testing
prepare:checkout the directory which contains the application used for testing
for example: I have download the test_sample2 to the directory d:/test/test_sample2.war

1).Update the admin-util.jar and deployment-admin.jar to the directory $GF_HOME/modules

2).Add the apache-commons-net.jar to the directory $GF_HOME/modules

3).If you need to set the proxy because of the company security, you need to set following configuration in GF_HOME/domains/domain1/config/domain.xml:

 <jvm-options>http.proxyHost=XXXXX</jvm-options>
 <jvm-options>http.proxyPort=XXXXX</jvm-options>

4).asadmin start-domain

5).asadmin deployuri file:/d:/test/test_sample2.war(Be sure the application to be deployed must be on the same side of the server).

6).asadmin deployuri http://java.net/jira/secure/attachment/50467/test_sample1.war

7).Create a ftp server and execute the following command as "asadmin deployuri  ftp://username:password@host:21/test_sample1.war"

8).open the website about http://localhost:8080/test_sample1 and http://localhost:8080/test_sample2 whether it can be accessed successfully

##Important notice:

1).It can be deployed to the remote server using --host option.

2).It also can be deployed to the cluster or instance using --target option.

## GlassFish leader:
1). Hong Zhang： hong.hz.zhang@oracle.com

2). Tom Muller:  Tom.Mueller@oracle.com
