pipeline {
    agent any
    tools {
        maven 'maven_3.8.7'
    }
    stages {
        stage('Code Compilation') {
            steps {
                echo 'code compilation is starting'
                sh 'mvn clean compile'
                echo 'code compilation is completed'
            }
        }
        stage('Create web.xml') {
            steps {
                echo 'Creating web.xml'
                script {
                    def webXmlPath = 'src/main/webapp/WEB-INF/web.xml'
                    def webXmlContent = '''
                        <?xml version="1.0" encoding="UTF-8"?>
                        <web-app xmlns="http://java.sun.com/xml/ns/javaee"
                                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                                 xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
                                 version="3.0">
                            <!-- Add your web.xml configuration here -->
                        </web-app>
                    '''
                    writeFile file: webXmlPath, text: webXmlContent
                }
                echo 'web.xml created'
            }
        }
        stage('Code Package') {
            steps {
                echo 'code packing is starting'
                sh 'mvn clean package'
                echo 'code packing is completed'
            }
        }
    }
}
