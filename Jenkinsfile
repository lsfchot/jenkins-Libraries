@Library('jenkins-Libraries') _
def tools = new org.devops.tools()
pipeline {
    agent any
    options {
        timestamps()
        skipDefaultCheckout()
        disableConcurrentBuilds()
        timeout(time: 1, unit: 'HOURS')
    }
    stages {
         stage("并行"){
        failFast true
       parallel{ 
        //获取代码
        stage("GetCode"){
            steps {
                timeout(time: 5, unit: "MINUTES"){
                    script{
                        println('获取代码')
                        input id: 'Test', message: '是否继续', ok: '是', parameters: [choice(choices: ['a', 'b'], name: 'parament')], submitter: 'admin'
                    }
                }
            }
        }
        //构建
        stage("build") {
            steps {
                timeout(time: 20, unit: 'MINUTES'){
                    script{
                        println('构建')
                    }
                }
            }
        }
             }
         }
        //代码扫描
        stage("ScanCode"){
            steps {
                timeout(time: 30, unit: 'MINUTES'){
                    script{
                        println('代码扫描')
                        tools.PrintMes("this is my lib")
                    }
                }
            }
        }
    }

    post {
        always{
            script{
                println('always')
            }
        }

        success{
            script{
                currentBuild.description = '构建成功'
            }
        }

        failure{
            script{
                currentBuild.description = '构建失败'
            }
        }

        aborted{
            script{
                currentBuild.description = '构建取消'
            }
        }
    }
}
