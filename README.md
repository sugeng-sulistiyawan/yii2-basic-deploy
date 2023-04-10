# Yii2 Basic Deploy

Deploy Yii2 Basic Application to Server via SSH by RSync

## Config Example:

```
name: Build and Deploy

on:
  # Runs on pushes targeting the default branch
  push:
    branches:
      - main

jobs:
    build:
        name: Build and Deploy
        runs-on: ubuntu-latest
        steps:
            - name: Checkout Repository
              uses: actions/checkout@v3

            - name: Setup Environment
              uses: shivammathur/setup-php@v2
              with:
                php-version: '7.4'

            - name: Install Packages
              run: composer install --no-progress --prefer-dist --optimize-autoloader --no-interaction

            - name: Deploy to Server
              uses: sugeng-sulistiyawan/yii2-basic-deploy@main
              with:
                user: ${{ vars.USER }}
                host: ${{ vars.HOST }}
                port: ${{ vars.PORT }}   # optional
                path: ${{ vars.PATH }}
                owner: ${{ vars.OWNER }} # optional
              env:
                DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}

            - name: Apply Migration
                run: php yii migrate --interactive=0
```
