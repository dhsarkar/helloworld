node {
    stage ('scm checkout') {
        checkout([$class: 'GitSCM',
branches: [[name: '*/master']],
doGenerateSubmoduleConfigurations: false, extensions: [], 
submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/dhsarkar/helloworld.git']]])
                        }
                        
stage ('App build') {
    sleep 5
    sh 'mvn clean package'
                  }
//sh 'chomod 755 target/*.war'
// This step should not normally be used in your script. Consult the inline help for details.
stage ('deployment'){
    sleep 5
archive 'target/*.war'
sh 'cp target/*.war /opt/apache-tomcat-8.5.31/webapps/'
sh '/opt/apache-tomcat-8.5.31/bin/shutdown.sh'
sh '/opt/apache-tomcat-8.5.31/bin/startup.sh'
sh '/opt/apache-tomcat-8.5.31/bin/catalina.sh stop'
sh '/opt/apache-tomcat-8.5.31/bin/catalina.sh start'
}
}
