# Evidence checklist — Driftnet

The original screenshots are stored in the private [Driftnet Notion page](https://app.notion.com/p/3e584380466280b5a1d0dcfc63cc1b1a). Copy the relevant images into this repository before adding Markdown image links. Suggested location: `assets/evidence/`.

## Recommended evidence set

Use cropped terminal/browser screenshots with readable text. Keep one image per proof point where practical.

- [ ] `01-recon-ping.png` — target reachability check.
- [ ] `02-nmap-all-ports.png` — full TCP port-scan result.
- [ ] `03-service-enumeration.png` — service/version results for the exposed ports.
- [ ] `04-traversal-proof.png` — proof of reading a harmless, non-secret file outside the intended static directory.
- [ ] `05-account-enumeration.png` — account name discovery; redact unrelated usernames if needed.
- [ ] `06-ssh-foothold.png` — successful SSH session as `deploy`; show only the username/host context needed to prove access.
- [ ] `07-sudo-version.png` — `sudo` version evidence, plus OS/package details if available.
- [ ] `08-root-proof.png` — minimal proof of root access (for example, a redacted `id` output).
- [ ] `09-lab-complete.png` — optional CTF completion/flag proof, with the flag redacted if the platform rules require it.

## Before committing screenshots

1. **Never upload the recovered `id_ed25519` private key**, `key.txt`, credential files, tokens, passwords, or exploit output containing secrets.
2. Redact public IPs, VPN addresses, hostnames, usernames, personal paths, and unrelated machine details where disclosure is unnecessary.
3. Keep the screenshot focused; crop out unrelated browser tabs, desktop notifications, and account information.
4. Do not edit command output to imply a result that was not observed. If a screenshot is missing, leave it unchecked rather than recreating it.
5. Use neutral filenames and add one-line captions explaining what each image demonstrates.

## Add images to the README

After copying and reviewing an image, link it from the matching section using a relative path, for example:

```markdown
![Nmap service enumeration](assets/evidence/03-service-enumeration.png)
```

Only add the link once the file exists in the repository. The screenshots are intentionally not fabricated or linked to private Notion attachment URLs.
