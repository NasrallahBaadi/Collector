# AD BloodHound Collector Wrapper

An interactive Bash wrapper script designed to unify and simplify Active Directory (AD) data collection. 

## Why This Exists

If you spend time on internal network assessments or labs, you know the frustration: every BloodHound collection tool (`bloodhound-ce-python`, `NetExec`, `BloodyAD`, `RustHound`) uses a completely different syntax, unique flag naming conventions, and inconsistent argument structures. 

More importantly, **environment restrictions and protocol quirks mean collectors frequently fail unpredictably**—LDAP signing requirements, packet filters, or timeout issues will cause one tool to break while another succeeds. 

This script solves that by providing:
1. **Zero Syntax Guessing:** Pass your credentials once, and let an interactive menu handle the underlying tool flags.
2. **Instant Fallbacks:** If standard Python collection hangs or fails due to network constraints, instantly switch to NetExec, BloodyAD, or RustHound with a single keystroke.
3. **Automatic Time Sync:** Automatically syncs system time with the target domain controller via `rdate` before execution to prevent Kerberos/NTLM auth failures.

---

## Features

* **Interactive Menu (`fzf`):** Arrow-key selection interface to choose your preferred collector on the fly.
* **Time Drift Mitigation:** Runs `rdate -n` against the target domain to avoid clock-skew authentication errors.
* **Pre-Configured Commands:** Maps your credentials securely into optimized command strings for:
  * `bloodhound-ce-python` (Standard)
  * `NetExec` (`nxc`)
  * `BloodyAD` (Direct to BH)
  * `RustHound-CE` (High-speed)

---

## Prerequisites

Make sure you have `fzf`, `rdate`, and your desired collectors installed and available in your `$PATH`:
* `bloodhound-ce-python`
* `nxc` (NetExec)
* `bloodyAD`
* `rusthound-ce`

---

## Usage

Run the script by supplying your target IP, domain, credentials, and Domain Controller FQDN:

```bash
./bloodhound-collect -i <TARGET_IP> -d <DOMAIN> -u <USERNAME> -p <PASSWORD> -dc <DC_FQDN>
