# nuo-config

Version marker for the NU Online mobile app remote config. The app fetches Firebase Remote Config only when the remote version here is greater than the locally stored version — this prevents excessive fetches against the Firebase RC daily quota.

## Endpoints

- **Primary**: `https://cdn.jsdelivr.net/gh/NU-Online/nuo-config@main/version.json`
- **Fallback**: `https://raw.githubusercontent.com/NU-Online/nuo-config/main/version.json`

Both return: `{"version": <integer>}`

## Publish Flow

1. Publish parameter changes in Firebase Console
2. Bump the number in `version.json` and commit

The GitHub Actions workflow (`.github/workflows/purge.yml`) automatically purges the jsDelivr cache on push. Full propagation to CDN edges takes ~10–15 minutes.

## Verification

```bash
curl https://cdn.jsdelivr.net/gh/NU-Online/nuo-config@main/version.json
curl https://raw.githubusercontent.com/NU-Online/nuo-config/main/version.json
```

Both should return the same version after CDN propagation completes.

## Version History

See commit history: `git log version.json`

## Cost

- GitHub public repo: $0
- jsDelivr CDN: $0 (unlimited)
- **Total**: $0/month
