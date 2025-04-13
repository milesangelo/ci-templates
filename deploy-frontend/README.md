
### In any other repo (in same org or public), your .github/workflows/deploy.yml can call it like this:

``` yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy frontend to Linode
        uses: your-org/ci-templates/deploy-frontend@v1
        with:
          docker_image_name: my-ui
          docker_container_name: my-ui
          port: "3000"
          env_vars: |
            NODE_ENV=production
            API_BASE_URL=${{ secrets.API_BASE_URL }}
            NEXTAUTH_SECRET=${{ secrets.NEXTAUTH_SECRET }}
```

✅ Note: your-org/ci-templates/deploy-frontend@v1 refers to a public repo, or a private repo in the same organization.


If It’s Private and Cross-Org…

You’ll need to:
	•	Make the ci-templates repo public or
	•	Use a personal access token (PAT) or fine-grained PAT with read:packages, and add it as a secret in the repo using the action.

https://github.com/settings/tokens
https://github.com/settings/tokens?type=beta

In that case:

```yaml
- name: Checkout template action
  uses: actions/checkout@v3
  with:
    repository: your-org/ci-templates
    token: ${{ secrets.CI_TEMPLATES_PAT }}
```

Then reference the local path if you clone it in a subdir.