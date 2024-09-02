---
title: Build and Deploy a Web Site with Github Action
published: 2024-09-02
tags: [Blogging, Demo, Website, Github]
category: Website
draft: true
---

In this guide, we will show you how to build and deploy a blog with Github Action.

# Step 1: Create two repository, public and private

For example, if we have a public repository named 'web_site' and a private repository named 'resource', we can write workflow in 'resource' to build and deploy the blog in 'web_site'.

We need to create '.github/workflows/build.yml' in 'resource' repository, and the content is as follows:

```yaml

on:
  push:
    branches: [ "main" ]
  workflow_dispatch:  # 手动触发

permissions:
  contents: read  

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: npm install, build.yml, and test
        run: |
          npm install -g pnpm
          pnpm install
          pnpm build

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          deploy_key: ${{ secrets.DEPLOY_TOKEN }} # 另外还支持 github_token 和 personal_token
          external_repository: xh-a/home # 修改为你的 GitHub Pages 仓库
          publish_dir: ./dist
          keep_files: false
          publish_branch: main
``` 
The config use 'actions/checkout@v4' to pull the code, and use 'peaceiris/actions-gh-pages@v3' to deploy the code to 'web_site' repository.

# Step 2: Generate a deploy token

GitHub Pages action support three types of token: 'github_token', 'personal_token', 'deploy_key'.
In this case, we use 'deploy_key' to deploy the code.
First, we need to create public and private key pair, and we can use the following command to generate the key pair:

```bash
ssh-keygen -t rsa -b 4096 -C "$(git config user.email)" -f gh-pages -N ""
# You will get 2 files:
#   gh-pages.pub (public key)
#   gh-pages     (private key)
```

Then, we need to add the public key to 'web_site' repository, and add the private key to 'resource' repository as a secret named 'DEPLOY_TOKEN'.

We can set public key in the web page of 'web_site' repository by visiting 'Settings' -> 'Deploy keys' -> 'Add deploy key', and paste the content of 'gh-pages.pub' to the input box with random title and check 'Allow write access'.

Then we can add the private key to 'resource' repository by visiting 'Settings' -> 'Secrets and variables' -> 'New repository secret', and paste the content of 'gh-pages' to the input box with the name 'DEPLOY_TOKEN'.

Now, we can push the code to 'resource' repository, and the workflow will be triggered to build and deploy the code to 'web_site' repository.
