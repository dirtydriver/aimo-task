
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

    sh "docker build -t ${tag}:0.1 . "

}

void buildCpp(){
    def image = docker.image("yaml-cpp-builder:0.1")
    image.inside{
        sh """
            mkdir build
            cd build
            cmake ..
            make
            make install
            cat yaml-cpp.pc
            tar -cvpf yaml-cpp-0.1.2.tar.gz *
            mv yaml-cpp-0.1.2.tar.gz $WORKSPACE
        """
    }   
}


node('slave'){

        stage('Clean Workspace'){
            deleteDir()
        }
        stage('Pull Own Source Code'){
                dir('Task'){
                pullsource("https://github.com/dirtydriver/aimo-task.git")
                buildImage("yaml-cpp-builder")
                }   
        }
          stage('Pull Yaml CPP Source Code & Build'){
                dir('Yaml'){
                pullsource("https://github.com/jbeder/yaml-cpp.git")
                buildCpp()
                }
        }     
}