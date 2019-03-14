stage("Build") {
    node('test-dynamic-slave') {
        println(scm.userRemoteConfigs)
        cleanWs()

        sfScmInfo = checkout([$class: 'GitSCM',
            branches: [[name: '*']],
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
    }
}

def makeTestStep(iteration) {
    return {
        node("test-dynamic-slave") {

            sfScmInfo = checkout([$class: 'GitSCM',
                branches: [[name: '*']],
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
            sh """
                |set +x
                |export GIT_SPECIFIER=${scmInfo.GIT_COMMIT}
                |rm -rf venv
                |virtualenv-3.4 venv
                |source venv/bin/activate
                |pip3 install docker-compose
                |docker-compose --version
                |git config --global user.name jenkins
                |git config --global user.email fdb-devs@snowflake.net
                |cd snowflake/jenkins
                |./build.sh configure download test sql sql_upload > \$WORKSPACE/iteration_${iteration}.log 2>&1
                |cat \$WORKSPACE/iteration_${iteration}.log
              """.stripMargin()
              archiveArtifacts 'iteration_*log'
        }
    }
}

stage("Test") {
    def testSteps = [:]
    for (int i = 0; i < 4; i++) {
        testSteps["Iteration ${i}"] = makeTestStep(i)
    }
    println(testSteps)

    parallel testSteps
}
