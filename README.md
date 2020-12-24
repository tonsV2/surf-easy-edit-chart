# Package chart
```bash
helm package --sign --key 'helm' --keyring ~/.gnupg/pubring.gpg .
```

# Push to repository
```bash
curl --user "$REPOSITORY_AUTH_USER:$REPOSITORY_AUTH_PASS" \
        -F "chart=@surf-easy-edit-1.3.0.tgz" \
        -F "prov=@surf-easy-edit-1.3.0.tgz.prov" \
        https://helm-charts.fitfit.dk/api/charts
```

# Backup
## Forward Postgresql port to localhost
```bash
k port-forward -n surf-easy-edit-prod surf-easy-edit-database-postgresql-0 5432:5432
```

## Dump database
```bash
pg_dump -h localhost -p 5432 -U easyedit easyedit > easyedit-(date "+%Y.%m.%d-%H.%M.%S").bak
```

# Migrate from Heroku to Kubernetes
## Backup
```bash
heroku pg:backups:url b001 --app surf-easyedit
```

## Download dump
```bash
heroku pg:backups:download --app surf-easyedit
```

## Forward postgresql port
```bash
k port-forward -n surf-easy-edit-prod surf-easy-edit-database-postgresql-0 5432:5432
```

## Restore
```bash
pg_restore --verbose --clean --no-acl --no-owner -h localhost -U easyedit -d easyedit latest.dump
```
