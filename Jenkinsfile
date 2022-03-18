@Library('jenkins-devops@dev')_ // load jenkins-devops as a library

properties([
  parameters([
    choice(      name: 'TYPE',              choices:     ['converge', 
                                                          'dismiss'],
                                            defaultValue: 'converge',        description: 'TYPE of run Deploy or Dismis packages'),
    string(      name: 'SERVICE',           defaultValue: 'rabbitmq',        description: 'Name of Service (also namespace too)'),
  ])
])

pipeline {
  agent { label 'werf' }

  environment {
    WERF_TMP_DIR                = '/home/jenkins/tmp/'
    WERF_HOME                   = '/home/jenkins/tmp/.werf/'
    WERF_IMAGES_REPO_MODE       = "monorepo"
    
    YC_REGISTRY                 = 'cr.yandex/xxxxxxxxx'
    AWS_REGISTRY                = 'xxxxxxxxx.amazonaws.com'
    WERF_STAGES_STORAGE         = "cr.yandex/xxxxxxxxx/${params.SERVICE}/stages"

    YC_AUTH                     = credentials("ya_registry_key")
    KUBECONFIG                  = credentials('werf_kube_config')
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage("Prerequisites") {
      steps {
        script {
          sh 'export'
        }
        script{
          functions.loginYCRegistry("${YC_AUTH}", "${YC_REGISTRY}")
        }
      }
    }
    stage("DEV") {
      when {
        anyOf { branch 'dev'; }
      }
      environment {   
        WERF_IMAGES_REPO      = "${YC_REGISTRY}/${params.SERVICE}"
        WERF_NAMESPACE        = "${params.SERVICE}"
        WERF_ENV              = "dev"
        WERF_KUBE_CONTEXT     = "dev"
      }
      steps {
        script {
          functions.runWerf("${params.TYPE}")
        }
      }
    }
    stage("PROD YC") {
      when {
        anyOf { branch 'master'; }
      }
      environment {
        WERF_IMAGES_REPO      = "${YC_REGISTRY}/${params.SERVICE}"
        WERF_NAMESPACE        = "${params.SERVICE}"
        WERF_ENV              = "production"
        WERF_KUBE_CONTEXT     = "production"
      }
      steps {
        script {
          functions.runWerf("${params.TYPE}")
        }
      }
    }
    stage("PROD AWS") {
      when {
        anyOf { branch 'master'; }
      }
      environment { 
		    WERF_IMAGES_REPO      = "${AWS_REGISTRY}/${params.SERVICE}"
        WERF_NAMESPACE        = "${params.SERVICE}"
        WERF_ENV              = "aws-production"
        WERF_KUBE_CONTEXT     = "aws-production"
      }
      steps {
        script {
          functions.runWerf("${params.TYPE}")
        }
      }
    }
  }
}