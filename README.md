# GitLab CI runner that pushes to git

This GitLab CI runner image allows to deploy a GitLab project to a remote Git repo.

## How to use

1. Create `.gitlab-ci.yml`:

```yaml
image: lorneluo/gitlab-ci-git-push

deploy_to_production:
  type: deploy
  environment: 
    name: production
    url: http://example.com
  only:
    - master
  script: git-push SSH_PRIVATE_KEY user@git.host:repo
```

2. Go to GitLab > Project > Settings > CI/CD Pipelines > Secret Variables, and add a variable `SSH_PRIVATE_KEY`:

```
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```

## Pushing to a branch other than master

By default, `git-push` will push to branch `master` of a remote repository (that's what Dokku wants). You can override this with:

```console
git-push SSH_PRIVATE_KEY user@git.host:repo branch
```

## Not doing force push

By default, git push will be forced. You can disable force push by setting environment variable `DISABLE_FORCE_PUSH` to any value.
