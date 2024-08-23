# Creating a database backup

Piping gzip or zip to the mysqldump command will imediately zip the file.

```sh
mysqldump --single_transaction=true -h <hostname> -u <username> -p <db_name> | gzip > ~/db_export_$(date +\%Y\%m\%d_\%H\%M\%S).sql.gz
```

### Retrieving file from the server

```sh
rsync -r <host_inside_ssh_config>:~/<db_export_date> ~/Downloads/
```

> [!NOTE]  
> `scp` can also be used if rsync is not installed (which would be strange lol)
