pipeline {
	agent any
	tools {
		maven 'maven 3.9.9'
	}

	parameters {
		choice(name: 'DEPLOY_ENVIRONMENT', choices: ['ninguno', 'tomcat1', 'tomcat2'], description: 'Ambiente de despliegue')
	}

	stages {
		stage('PackageDocker') {
			steps {
				bat 'mvn -B -q -P docker-build clean package'
			}
		}
		stage('Deploy') {
			when {
				not {
					equals expected: 'ninguno', actual: params.DEPLOY_ENVIRONMENT
				}
			}
			steps {
				bat 'copy target\\ROOT.war D:\\devenv\\CURSOJENKINS\\ambientes\\' + params.DEPLOY_ENVIRONMENT + '\\apache-tomcat-9.0.96\\webapps\\'
			}
		}
	}
}
