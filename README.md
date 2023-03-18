<p align="center"><img src="https://statamic.com/assets/branding/Statamic-Logo+Wordmark-Rad.svg" width="400" alt="Statamic Logo" /></p>

## How to deploy to [fly.io](https://fly.io/)

1. Masuk ke repository local yang akan di deploy, lalu login dengan `fly auth login`
2. Buat token API dengan perintah `flyctl auth token`
3. Buat repository di Github -> Setting -> Secret and variable -> actions
4. Masukan token yang sudah dibuat di step ke 2 dan beri nama `FLY_API_TOKEN`
5. Jalankan perintah `flyctl launch`. Beri jawaban `N` untuk database dan jawaban `N` untuk deploy.
6. buat file `.github/workflows/fly.yml` dengan isi konten

```
name: Fly Deploy
on:
  push:
    branches:
      - main
jobs:
  deploy:
    name: Deploy app
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: superfly/flyctl-actions/setup-flyctl@master
      - run: flyctl deploy --remote-only
        env:
          FLY_API_TOKEN: ${{ secrets.FLY_API_TOKEN }}

```

7. Commit & push
8. Lalu buka repository Github -> action dan aplikasi akan deploy otomatis

## Important Links

- [Statamic Main Site](https://statamic.com)
- [Statamic 3 Documentation][docs]
- [Statamic 3 Core Package Repo][cms-repo]
- [Statamic 3 Migrator](https://github.com/statamic/migrator)
- [Statamic Discord][discord]

[docs]: https://statamic.dev/
[discord]: https://statamic.com/discord
[contribution]: https://github.com/statamic/cms/blob/master/CONTRIBUTING.md
[cms-repo]: https://github.com/statamic/cms
