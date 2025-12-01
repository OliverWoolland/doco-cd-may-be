# doco-cd-may-be
A quick test of doco-cd for automatically deploying github repos 

While generally `doco-cd.yml` and the doco-cd deployment compose file would live 
in different repos, they are bundled here to make everything needed obvious.

## Setup

Run these commands to setup doco-cd for your testing

```
cp env.template .env
nano .env # populate variables
# Put doco-cd up
docker compose -f doco-compose.yaml up -d
docker compose logs -f
```

## Additional convinence setup 

Read these commands carefully and understand what they do - they will not be useful
or desirable for everyone.
```
# Install github cli tool 
# Guide for specific distros: https://github.com/cli/cli/blob/trunk/docs/install_linux.md
curl -sS https://webi.sh/gh \| sh
# Obtain GIT_ACCESS_TOKEN
gh auth
echo GIT_ACCESS_TOKEN=$(gh auth token) > .env
# Grant testing webhook access
gh extension install cli/gh-webhook
gh webhook forward --repo=REPOSITORY --events=EVENTS --url=localhost:8543
#
``` 
