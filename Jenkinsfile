node {
    stage 'Clone the project'
    git 'https://github.com/eugenp/tutorials.git'

    dir('spring-jenkins-pipeline') {
        stage("Compilation and Analysis") {
            parallel 'Compilation': {
                if (isUnix()) {
                    sh "./mvnw clean install -DskipTests"
                } else {
                    bat "./mvnw.cmd clean install -DskipTests"
                }
            }, 'Static Analysis': {
                stage("Checkstyle") {
                    if (isUnix()) {
                        sh "./mvnw checkstyle:checkstyle"
                    } else {
                        bat "./mvnw.cmd checkstyle:checkstyle"
                    }
                     step([$class: 'CheckStylePublisher',
                          canRunOnFailed: true,
                          defaultEncoding: '',
                          healthy: '100',
                          pattern: '**/target/checkstyle-result.xml',
                          unHealthy: '90',
                          useStableBuildAsReference: true
                        ])
                }
            }
        }
		
		}
		}
