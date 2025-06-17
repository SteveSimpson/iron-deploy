# iron-deploy

Something to play with GitLab, Apache NiFi &amp; other services. I would not use this in production.

## Quick Up

### URLs

If you follow this guide, the following URLs will work:

* http://gitlab
* http://maildev

### Steps

1. Copy the .env.example files to .env
2. Update the example parameters to your taste
3. Update your hosts file (see below)
4. Run `docker compose up -d`
5. Wait... it will take a few minutes for things to set themselves up
6. After your coffee break,
7. Access Gitlab at http://gitlab:8088 login with root and the password you configured.

### Hosts file

In order to access services cleanly, and let things work, we are going to name a few things,
then alias the access to localhost on your local platform.
These instructions will work for Mac or Linux, but will need to be adapted for Windows.

Update `/etc/hosts`

You just need to update your localhost line to include the following.

```sh
127.0.0.1       localhost gitlab maildev nifi
```

### Setup to use maildev

After starting gitlab, edit the `./gitlab/config/gitlab.rb` file:

```rb
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "maildev"
gitlab_rails['smtp_port'] = 1025
gitlab_rails['smtp_enable_starttls_auto'] = false
gitlab_rails['smtp_tls'] = false
gitlab_rails['smtp_pool'] = false
```

Then get a shell in the container with with:
`docker compose exec gitlab bash`

In that shell run the following command to apply the configuration: 
`gitlab-ctl reconfigure`


## Shutdown and Cleanup



## Notes

* By default, data is stored locally under `./gitlab`, this means:
    * If you are using this for personal development, I would back this up to another drive or s3.
    * The data is excluded from this git project.
    * You can adjust where your data is stored by forking the repo and updating `docker-compose.yaml`.


