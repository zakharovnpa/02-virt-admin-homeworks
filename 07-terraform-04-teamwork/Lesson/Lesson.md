### Выполнение ДЗ по теме "7.4. Средства командной работы над инфраструктурой."

##### Создай `server.yaml` который скажет атлантису:
1. Укажите, что атлантис должен работать только для репозиториев в вашем github (или любом другом) аккаунте.
2. На стороне клиентского конфига разрешите изменять `workflow`, то есть для каждого репозитория можно будет указать свои дополнительные команды. 
3. В `workflow` используемом по-умолчанию сделайте так, что бы во время планирования не происходил `lock` состояния.

```yml
# repos lists the config for specific repos.
repos:

  # id can either be an exact repo ID or a regex.
  # If using a regex, it must start and end with a slash.
  # Repo ID's are of the form {VCS hostname}/{org}/{repo name}, ex.
  # github.com/runatlantis/atlantis.
- id: /.*/
  # branch is an regex matching pull requests by base branch
  # (the branch the pull request is getting merged into).
  # By default, all branches are matched
  branch: /.*/

  # apply_requirements sets the Apply Requirements for all repos that match.
  apply_requirements: [approved, mergeable]

  # workflow sets the workflow for all repos that match.
  # This workflow must be defined in the workflows section.
  workflow: custom

  # allowed_overrides specifies which keys can be overridden by this repo in
  # its atlantis.yaml file.
  allowed_overrides: [apply_requirements, workflow, delete_source_branch_on_merge]

  # allowed_workflows specifies which workflows the repos that match 
  # are allowed to select.
  allowed_workflows: [custom]

  # allow_custom_workflows defines whether this repo can define its own
  # workflows. If false (default), the repo can only use server-side defined
  # workflows.
  allow_custom_workflows: true

  # delete_source_branch_on_merge defines whether the source branch would be deleted on merge
  # If false (default), the source branch won't be deleted on merge
  delete_source_branch_on_merge: true
  
  # pre_workflow_hooks defines arbitrary list of scripts to execute before workflow execution.
  pre_workflow_hooks: 
    - run: my-pre-workflow-hook-command arg1

  # id can also be an exact match.
- id: github.com/myorg/specific-repo

# workflows lists server-side custom workflows
workflows:
  custom:
    plan:
      steps:
      - run: my-custom-command arg1 arg2
      - init
      - plan:
          extra_args: ["-lock", "false"]
      - run: my-custom-command arg1 arg2
    apply:
      steps:
      - run: echo hi
      - apply
      
```
##### Создай `atlantis.yaml` который, если поместить в корень terraform проекта, скажет атлантису:
1. Надо запускать планирование и аплай для двух воркспейсов `stage` и `prod`.
```yml

```
2. Необходимо включить автопланирование при изменении любых файлов `*.tf`.
```yml

```
