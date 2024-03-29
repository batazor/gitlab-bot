# gitlab-bot

Automation of routine operations in GitLab (issue && MR lifecycle)

### How add to my project?

**1. Add this proejct as git submodule**

```
git submodule add git@<URL>/gitlab-bot.git ops/policy
```

**2. Add ENV variables**

`GITLAB_HOST_URL` - GitLab address `https://gitlab.com`  
`GITLAB_API_TOKEN` - token for GitLab API  
`PATH_TO_POLICY` - path to policy into your project (default: `/ops/policy`)  
`TYPE_SOURCE` - `project` or `groups` (default: `groups`)

**3. Include gitlab-bot-template to `.gitlab-ci.yml`**

> docs: https://docs.gitlab.com/ee/ci/yaml/#include

**.gitlab-ci.yaml**
```yaml
# include template
include:
  - project: '<groupName>/gitlab-bot'
    ref: master
    file: '/templates/issue.yml'

# Add stage
stages:
  - triage
```

**4. Add jobs to schedule for project**

> docs: https://docs.gitlab.com/ee/user/project/pipelines/schedules.html

Add variables:
- `RUN_DAILY: true` - for everyday `gitlab-bot (every day)`
- `RUN_WEEKS: true` - for weeks `gitlab-bot (every week)`
- `RUN_MONTH: true` - for month `gitlab-bot (every month)`

**5. Add labels to project/group**

+ `needs attention` - bot add this a label to issue for *attention*

### Update

```
git submodule sync --recursive
git submodule update --init --recursive
git submodule foreach git pull origin master
```


### Run in dev mode

```
docker run -it -v "$(pwd)":/src ruby:2.4-alpine sh
> gem install gitlab-triage --no-doc
> gitlab-triage -H $GITLAB_HOST_URL -f $GITLAB_TRIAGE_FILE --source groups --token $GITLAB_API_TOKEN --source-id $CI_PROJECT_ID
```
