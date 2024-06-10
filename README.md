# WordPress Stack

Create a fully functioning WordPress Stack with NGiNX, MariaDB, and WordPress ( including Composer and WP-CLI ) using Ansible and Docker.

![Stack](stack.webp)
 
## Prerequisites

Applications needed will be:

- Docker Hub or Podman Desktop
- Docker CLI ( or Podman CLI )
- Visual Studio Code or equivilent code editor
- A Docker or Quay.io ( RedHat ) account to create repositories.
- Minikube and kubernetes-cli.

## Build

Individually, the images can be built, tagged, and pushed to a repo for easy access.

1. docker build -f Dockerfile -t [name] .
2. docker image tag [name]:latest [repo]/[name]:[version]
3. docker push [repo]/[name]:[version]

Or, using Ansible to automate the process:

```bash
ansible-playbook images.yaml -i ~/inventory.yaml
```

### Extras

MariaDB requires a `.env` file with the following values:

```bash
DB_NAME=''
DB_USER=''
DB_PASSWORD=''
DB_ROOT_PASSWORD=''
DB_HOST=''
WP_ENV=''
WP_HOME='http://'
WP_SITEURL='http://wp'

# Generate your keys here: https://roots.io/salts.html
AUTH_KEY=''
SECURE_AUTH_KEY=''
LOGGED_IN_KEY=''
NONCE_KEY=''
AUTH_SALT=''
SECURE_AUTH_SALT=''
LOGGED_IN_SALT=''
NONCE_SALT=''
```

## Run

Create the deployments all at once:

```bash
ansible-playbook deployment.yaml -i ~/inventory.yaml
```

Then create the bedrock project:

```bash
ansible-playbook bedrock.yaml -i ~/inventory.yaml
```

Finally, navigate to the site:

```bash
minikube service nginx
```

You should see the WordPress install screen:

![Install](install.webp)