pipeline 
{
    agent any
    stages
    {
        stage ('Build Backend')
        {
            steps
            {
                bat 'mvn clean package -DskipTests=true'
            }
        }

        stage ('Unit Tests')
        {
            steps
            {
                bat 'mvn test'
            }
        }

        stage ('Sonar Analysis')
        {
            environment 
            {
                scannerHome = tool 'SONAR_SCANNER'
            }

            steps
            {
                script
                {
                    scannerHome.replace(" ", "^")
                    bat echo scannerHome
                } 
                withSonarQubeEnv('SONAR_LOCAL')
                {
                    bat "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.login=5b503bd807a047a8052198b8aaab046bb7bfbf6c -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java"
                }
            }
        }
    }
}