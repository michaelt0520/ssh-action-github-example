# 🚀 SSH for GitHub Actions
[GitHub Action](https://github.com/appleboy/ssh-action) for executing remote ssh commands.

![](https://github.com/appleboy/ssh-action/raw/master/images/ssh-workflow.png)

## Usage
**Executing remote ssh commands.**

```
name: remote ssh command
on: [push]
jobs:

  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
    - name: executing remote ssh commands using password
      uses: appleboy/ssh-action@master
      with:
        host: ${{ secrets.HOST }}
        username: ${{ secrets.USERNAME }}
        password: ${{ secrets.PASSWORD }}
        port: ${{ secrets.PORT }}
        script: whoami
```

output:

```
======CMD======
whoami
======END======
out: ***
==============================================
✅ Successfully executed commands to all host.
==============================================
```

### Input variables
See action.yml for more detailed information.

- **host** - ssh host
- **port** - ssh port, default is 22
- **username** - ssh username
- **password** - ssh password
- **passphrase** - the passphrase is usually to encrypt the private key
- **sync** - synchronous execution if multiple hosts, default is false
- **timeout** - timeout for ssh to remote host, default is 30s
- **command_timeout** - timeout for ssh command, default is 10m
- **key** - content of ssh private key. ex raw content of ~/.ssh/id_rsa
- **key_path** - path of ssh private key
- **script** - execute commands
- **script_stop** - stop script after first failure
- **envs** - pass environment variable to shell script
- **debug** - enable debug mode

### Example
**Executing remote ssh commands using password.**

```
- name: executing remote ssh commands using password
  uses: appleboy/ssh-action@master
  with:
    host: ${{ secrets.HOST }}
    username: ${{ secrets.USERNAME }}
    password: ${{ secrets.PASSWORD }}
    port: ${{ secrets.PORT }}
    script: whoami
```

**Using private key**

```
- name: executing remote ssh commands using ssh key
  uses: appleboy/ssh-action@master
  with:
    host: ${{ secrets.HOST }}
    username: ${{ secrets.USERNAME }}
    key: ${{ secrets.KEY }}
    port: ${{ secrets.PORT }}
    script: whoami
```

**Multiple Commands**

```
- name: multiple command
  uses: appleboy/ssh-action@master
  with:
    host: ${{ secrets.HOST }}
    username: ${{ secrets.USERNAME }}
    key: ${{ secrets.KEY }}
    port: ${{ secrets.PORT }}
    script: |
      whoami
      ls -al
```

![](https://github.com/appleboy/ssh-action/raw/master/images/output-result.png)
