
void pullsource(String url,String branch = null){
    String repo_branc= branch ?: "master"
        checkout([
			$class: 'GitSCM',
			branches: [[name: "${repo_branc}"]],
			doGenerateSubmoduleConfigurations: false,
			extensions: [],
			submoduleCfg: [],
			userRemoteConfigs: [[
				credentialsId: 'Github',
				url: "${url}"
			]]
        ])
    
}

void buildImage(String tag){

    sh "docker build -t ${tag} . "

}


node('slave'){
        stage('Pull Source Code'){
                dir('Task'){
                pullsource("https://github.com/dirtydriver/aimo-task.git")
                buildImage("yaml-cpp-builder")
                }
            
        }
          stage('Build Docker Image'){
                sh 'ls -l'
            
        }
        stage('Check Docker Binary'){
                sh 'which docker'
            
        }
        
}