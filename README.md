# S3 backup for Docker

A docker container to backup an S3 bucket to another bucket or SFTP server.

## Configuration

Create a configuration file as described in the [ten7.s3_backup](https://github.com/ten7/s3-backup) Ansible role.

Once created, you have three ways to provide it to the container:
* As a base64-encoded value of the `S3_BACKUP_CONFIG` environment variable
* As a mounted file at the location specified by the `S3_BACKUP_CONFIG_FILE` environment variable
* As a mounted file at `/config/s3-backup/s3-backup.yml` inside the container.

## Use with base Docker

To run the Docker image as part of a script or in cron, use the following command:

```shell
docker run --rm -v /path/to/s3-backup.yml:/config/s3-backup/s3-backup.yml ten7/s3-backup
```

Note, that if your `s3-backup.yml` file depends on other files (such as SSH keys) you will need to add multiple `-v` switches to mount each one.

## Docker compose

Create the following Docker Compose file.

```yaml
version: '3'
services:
  backup:
    image: ten7/s3-backup
    volumes:
      - /path/to/s3-backup.yml:/config/s3-backup/s3-backup.yml
```

Again, if your `s3-backup.yml` depends on other files (such as SSH keys) you will need to add additional items under `volumes` to mount them.

Once the `docker-compose.yml` file is created, you can run backups using:

```shell
docker-compose run backup
```

## License

GPL v3

## Author Information

This Docker image was created by [TEN7](https://ten7.com/).

