node('test-dynamic-slave') {
    stage("Checkout") {
        println("${scm}")
        println("${scm.branches}")
        cleanWs()

        sfScmInfo = checkout([$class: 'GitSCM', 
            branches: [[name: '*/master']], 
            doGenerateSubmoduleConfigurations: false, 
            extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'snowflake']],
            submoduleCfg: [], 
            userRemoteConfigs: [[credentialsId: 'a0395839-84c7-4ceb-90e2-bcf66b2d6885', url: 'ssh://bitbucket-internal.int.snowflakecomputing.com:7999/opfdb/fdb_snowflake.git']]
            ])
        println("$sfScmInfo")

        scmInfo = checkout([
            $class: 'GitSCM',
            branches: scm.branches,
            doGenerateSubmoduleConfigurations: scm.doGenerateSubmoduleConfigurations,
            extensions: scm.extensions,
            userRemoteConfigs: scm.userRemoteConfigs,
            extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'snowflake/jenkins/foundationdb']]
            ])
        println("$scmInfo")
    }
    stage("Build") {
        /*
        sh """
            |export GIT_SPECIFIER=${scmInfo.GIT_COMMIT}
            |rm -rf venv
            |virtualenv-3.4 venv
            |source venv/bin/activate
            |pip3 install docker-compose
            |docker-compose --version
            |git config --global user.name jenkins
            |git config --global user.email fdb-devs@snowflake.net
            |cd snowflake/jenkins
            |./build.sh check_uploaded package upload
          """.stripMargin()
        */
    }
}
