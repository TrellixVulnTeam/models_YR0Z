node {
    sshagent (credentials: (env.DMAKE_JENKINS_SSH_AGENT_CREDENTIALS ?
                            env.DMAKE_JENKINS_SSH_AGENT_CREDENTIALS : '').tokenize(',')) {
        if (params.CLEAR_WORKSPACE) {
            deleteDir()
        }
        echo 'BUILD_TAG:'
        echo BUILD_TAG
        echo "models:${BUILD_TAG}"
        checkout([$class: 'GitSCM',
                  branches: scm.branches,
                  extensions: scm.extensions + [[$class: 'SubmoduleOption', recursiveSubmodules: true]],
                  userRemoteConfigs: scm.userRemoteConfigs])

        docker.build("models:jenkins-models-PR-19-900")
    }
}
