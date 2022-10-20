# Youappz Deploy Action

This action for [Youappz](https://sitez.youappz.com/) builds your Jamstick project for [Youappz](https://sitez.youappz.com/).

For more information, please see our complete deployment guide—[Deploy your Astro Site to GitHub Pages](https://docs.astro.build/en/guides/deploy/github/).

## Usage

> **Note**: Want to get started even faster? Create a repository from our official [GitHub Pages template](https://github.com/withastro/github-pages)!

### Inputs

- `path` - Optional: the root location of your project inside the repository.
- `node-version` - Optional: the specific version of Node that should be used to build your site. Defaults to `16`.
- `package-manager` - Optional: the Node package manager that should be used to install dependencies and build your site. Automatically detected based on your lockfile.

### Example workflow:

#### Build and Deploy to Youyappz

Create a file at `.github/workflows/deploy.yml` with the following content.

```yml
name: Deploy to Youappz

on:
  # Trigger the workflow every time you push to the `main` branch
  # Using a different branch name? Replace `main` with your branch’s name
  push:
    branches: [main]
  # Allows you to run this workflow manually from the Actions tab on GitHub.
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout your repository using git
        uses: actions/checkout@v3
      - name: Install, build, and upload your site output
        uses: youappz/action@v0
        # with:
        # path: . # The root location of your project inside the repository. (optional)
        # node-version: 16 # The specific version of Node that should be used to build your site. Defaults to 16. (optional)
        # package-manager: yarn # The Node package manager that should be used to install dependencies and build your site. Automatically detected based on your lockfile. (optional)

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v1
```
