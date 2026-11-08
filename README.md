# DryGuard

Private setup page for DryGuard, hosted on GitHub Pages.

The page is encrypted, so `index.html` in this repo contains no readable content. It can only be opened with the private link or the password.

## How it works

- [StaticCrypt](https://github.com/robinmoisson/staticrypt) encrypts the page with AES-256 before it is committed.
- GitHub Pages serves the encrypted `index.html` from the `main` branch.
- The private link carries the key after the `#`, which browsers do not send to the server. The page is decrypted in the visitor's browser.
- Without the key, visitors only see a password prompt.

The unencrypted page and the password are not stored in this repo.

## Updating the page

Edit the unencrypted copy, then encrypt it with the original password and salt so the existing link keeps working:

```
npx staticrypt@3 _source/index.html -p <password> -s <salt> --config false -d .
```

Commit and push the new `index.html`. Never commit the unencrypted page, because Git history keeps it permanently.
