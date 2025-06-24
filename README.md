# google-drive-upload-action (forked from [`adityak74`][original_repo])

[![build](https://github.com/BEES-Group/google-drive-upload-git-action/actions/workflows/ci.yaml/badge.svg?branch=main)](https://github.com/adityak74/google-drive-upload-git-action/actions)

Github action that uploads files to Google Drive.

Please consult the [original_repo] for further instruction

## Additional Features

- Use prebuilt image
- Support windows base action

## Usage Example

In this example we stored the folderId and credentials as action secrets. This is highly recommended as leaking your credentials key will allow anyone to use your service account.

```yaml
# .github/workflows/upload.yml
on: { push: { branches: [main, dev] } }

jobs:
  upload:
    runs-on: ubuntu-latest
    steps:
      - name: 🛎 Checkout
        uses: actions/checkout@v4
      - name: 📦 Create Archive
        run: git archive --output=source.zip HEAD && md5sum source.zip
      - name: ☁️ Upload to Google Drive
        uses: beesgroup/google-drive-upload-git-action
        with:
          credentials: ${{ secrets.GOOGLE_DRIVE_CREDENTIALS }}
          folderId: ${{ secrets.GOOGLE_DRIVE_FOLDER_ID }}
          filename: source.zip
          name: source-${{ github.ref_name }}.zip # optional
          overwrite: "true" # optional boolean
```

[original_repo]: https://github.com/adityak74/google-drive-upload-git-action
