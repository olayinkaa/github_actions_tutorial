### [GITHUB ACTIONS](https://docs.github.com/en/actions)
- [Event trigger](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)

- [Github Context](https://docs.github.com/en/actions/learn-github-actions/contexts)
- []

### RUNNER
- Any machine with the github actions runner application installed
- It is responsible for runner your job whenever an event happens and display back the result
- It can be hosted by github or you host your own runner

Github hosted runners: l
- inux, window or macOs virtual environments with commonly-used pre-installed software.
- Maintained by github
- You cannot customised the hardware configuration

Self-hosted runners
- Machine you manage and maintain with the runner application installed

### SECRET
- ACTIONS_RUNNER_DEBUG : true
- ACTIONS_STEP_DEBUG : true

### NOTE
- windows VM runs on powershell by default

## SAMPLE 
```js
on: 
    push:
    pull_request:
        types: [closed,assigned, reopened, opened]  //activity type
```

```js
on: 
    schedule:
        - cron: "* * * *" // https://crontab.guru/
```

### MANUAL TRIGGER
[Use the REST API to manage repositories on GitHub.](https://docs.github.com/en/rest/repos/repos?apiVersion=2022-11-28#get-a-repository)
-  https://api.github.com/repos/{repo_username}/{repo_project_name}/dispatches

```js
on:
    repository_dispatch:
    push:
        branches:
            - master
            - "feature/**"
            - '!feature/featC'
        branches-ignore:
            - test-branch
        tags:
            - v1.*
        tags-ignore:
            - v2.*
        paths:
            - '**.js'
        paths-ignore:
            - 'doc/**'
```

### ENVIRONMENT VARIABLES
- [Default Environment Variable](https://docs.github.com/en/actions/learn-github-actions/variables)
```js
name: Environment variable
on: push
env:
    WF_ENV: Available on all jobs
    log_token:: ${{secrets.token}} // from github secrets
jobs:
    log_env:
        runs-on: ubuntu-latest
        env:
            JOB_ENV: available on this job
        steps:
            - name: log env values
              env: 
                STEP_ENV: available only on this step
              run: |
                echo "WF_ENV: ${WF_ENV}"
                echo "JOB_ENV: ${JOB_ENV}"
                echo "STEP_ENV: ${JOB_ENV}"
                echo "GITHUB REPO: ${GITHUB_REPOSITORY}"
```