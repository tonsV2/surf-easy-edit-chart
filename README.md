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
