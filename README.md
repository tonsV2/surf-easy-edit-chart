# Package chart
```bash
helm package --sign --key 'helm' --keyring ~/.gnupg/pubring.gpg .
```

# Push to repository
```bash
curl --user "user:pass" \
        -F "chart=@surf-easy-edit-1.0.0.tgz" \
        -F "prov=@surf-easy-edit-1.0.0.tgz.prov" \
        https://helm-charts.fitfit.dk/api/charts
```
