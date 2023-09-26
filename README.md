# Terraform Beginner Bootcamp 2023

## Semantic versioning :mage:

This project is going to utilize semantic versioning for its tagging. [semver.org/](https://semver.org/)

The general format
**MAJOR.MINOR.PATCH**, e.g `1.0.1`:

- **MAJOR** version when you make incompatible API changes
- **MINOR** version when you add functionality in a backward compatible manner
- **PATCH** version when you make backward compatible bug fixes


## Install Terraform CLI

The terraform CLI installation instructions have changed due to gpg keyring changes. So we needed to refer to the latest install CLI instructions via Terraform Documentation and change the scripting for install.

### Refactoring into Bash Scripts

While fixing the terraform CL gpg depreciation issues we notices that the bash scripts steps were considerable amount more codes. So we decided to create a bash scripts to install the terrafom CLI. 

This bash scripts is located here: [./bin/install_ terraform_cli](./bin/install_terraform_cli)

- This will keep the Terraform Gitpod Task File ([.gitpod.yml](.gitpod.yml)) tidy.
- This allow us an easier to debug and execute manually Terraform CLI install.
- This wil allow better portability for other projects that need to install Terraform CLI.


### Shebang Consideration
A shebang (pronounced Sha-bang) tells the bash scripts what program that will interprete the scripts. e.g `#!/bin/bash`

ChatGPT recommends this format for bash: 
`#!/usr/bin/env bash`

- for portability for different OS distributions.
- will search the user's PATH for the bash executable.

### Execution Consideration
When executing the bash we can use the `./` shorthand notation to execute the bash scripts.

e.g `./bin/install_terraform_cli`
If we are using a script in .gitpod.yml we need to point the script to a program to interprete it.

e.g `source .bin/install_terraform_cli`

#### Linux Permissions Consideration

In order to make the bash script executable, we need to change the linx permission for the fix to be executable at the user mode.

```sh
chmod u+x ./bin/install_terraform_cli
```


Alternatively,
chmod 744 ./bin/install_terraform_cli


### Github Lifecycle (Before, Init, Command)

We ned to be carefull when we use init because it will not rerun if we restart an existing workspace.


### Working Env Vars


### env command

We can list out all environment variables (Env Vars) using the `env` command.

We can filter specific env vars using grep e.g `env | grep AWS_`

### Setting and Unsetting Env Vars

In the terminal we can set using `export HELLO='world`

In the terminal we unset using `unset HELLO`

We can set an env var temporarily when just running a command

```sh
HELLO='world' ./bin/print_message
```

Within a bash script we can set env without writing export e.g

```sh

#!/usr/bin/env bash

HELLO='world'

echo $HELLO
```

#### Printing Vars

We can print an env vars using  echo e.g `echo $HELLO`


#### Scoping of Env Vars

When you open up new bash terminals in the VSCode it will not be aware of env vars that you have set in another window.

If you want Env Vars to persist across all future bash terminals that are open you need to set env vars in your bash profile. e.g `.bash_profile`

#### Persisting Env Vars in Gitpod

We can persist env vars into gitpod by storing them in Gitpod secrets storage.

```
gp env HELLO='world'
```


All futre workspaces launched will set the env vars for all bash terminals opened in those workspaces.

You can also set env vars in the `gitpod.yml` but this can only contain non-sensitive env vars.


[Install Terraform CLI](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)


https://en.wikipedia.org/wiki/File-system_permissions

https://en.wikipedia.org/wiki/Chmod

https://www.gitpod.io/docs/configure/workspaces/tasks