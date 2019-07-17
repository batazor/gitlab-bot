# gitlab-bot

### How add to my project?

**1. Add this proejct as git submodule**

```
git submodule add git@code.rightech.io:rightech-devops/gitlab-bot.git ops/policy
```

**2. Add ENV variables**

`GITLAB_API_TOKEN` - token for GitLab API
`PATH_TO_POLICY` - path to policy into your project (default: `/ops/policy`)

**3. Include gitlab-bot-template to `.gitlab-ci.yml`**

> docs: https://docs.gitlab.com/ee/ci/yaml/#include

**.gitlab-ci.yaml**
```yaml
# include template
include:
  - project: 'rightech-devops/gitlab-bot'
    ref: master
    file: '/templates/issue.yml'

# Add stage
stages:
  - triage
```

**4. Add jobs to schedule for project**

> docs: https://docs.gitlab.com/ee/user/project/pipelines/schedules.html

**5. Add labels to project/group**

+ `needs attention` - bot add this a label to issue for *attention*

### Update

```
git submodule sync --recursive
git submodule update --init --recursive
git submodule foreach git pull origin master
```
