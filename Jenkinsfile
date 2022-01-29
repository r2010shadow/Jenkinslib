#groovy

@Libary('jenkinslib') _

def tools = new org.devops.tools()

String workspace = "/opt/jenkins-data/workspace"

//Pipeline
pipeline {
	agent any
	
	options {
		timestamps()
		skipDefaultCheckout()
		disableConcurrentBuilds()
		timeout(time:1, unit:'HOURS')
	}
	
	stages {
		stage("GetCode"){
			when { environment name: 'test', value: 'abcd' }
			steps{
				timeout(time:5, unit:"MINUTES"){
					script{
						println('获取代码')
						println('${test}')
					
						// input id: 'Test', message: '我们是否继续?',ok:'是，继续.',parameters:
					}
				}
			}
		}
		
		stage("01"){
			failFast true
			parallel {
				
				// goujian 
				stage("Build"){
					steps{
						timeout(time:20, unit:"MINUTES"){
							script{
								println("应用打包")
								
								mvnHome = tool "m2"
								println(mvnHome)
								
								sh "$(mvnHome}/bin/mvn --version"
							}
						}
					}
				}
				
				stage("CodeScan"){
					steps{
						timeout(time:30, unit:"MINUTES"){
							script{
								println("代码扫描")
								
								tools.PrintMes("This is my lib.")
							}
						}
					}
				}
			}
			
		}
		
		post {
			always {
				script{
					println("always")
				}
			}
			
			success {
				script{
					currentBuild.description = "\n 构建成功"
				}
			}
			
			faiure {
				script{
					currentBuild.description = "\n 构建失败"
				}				
			}
			
			aborted {
				script{
					currentBuild.description = "\n 构建取消"
				}					
			}
		}
		
	}
	
}
