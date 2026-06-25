# Windows Server RDS Learning Path 53 — Troubleshoot RDS Domain Join Failures

**Level:** Expert · **Module:** 53/70

## Goal
Diagnose a lab server that cannot join `corp.lab` by using DNS, time, network, computer-object, and setup-log evidence.

## Procedure
1. Record the exact error and time.
2. Confirm the server uses `10.30.30.10` as DNS.
3. Resolve the domain and AD service records.
4. Compare time with DC01.
5. Test network access to DC01.
6. Check for an existing or disabled computer object with the same name.
7. Review the Windows domain-join setup log.
8. Correct the identified cause, retry once, and validate the secure channel.

```powershell
Get-DnsClientServerAddress -AddressFamily IPv4
Resolve-DnsName -Type SRV _ldap._tcp.dc._msdcs.corp.lab
w32tm.exe /stripchart /computer:dc01.corp.lab /samples:5 /dataonly
Get-Content $env:windir\debug\NetSetup.log -Tail 200
Test-ComputerSecureChannel -Verbose
```

## Evidence
Store the original error, DNS/time/network checks, sanitized setup-log excerpt, computer-object state, root cause, corrective action, and successful post-fix result under `evidence/`.

## Troubleshooting
Collect evidence before changing the computer object. DNS and time should be validated first.

## Security
Use only approved lab administration and remove real organization details from published evidence.

## Rollback
Restore the disposable server to its pre-join state only after exporting diagnostics.

## Next
`Windows-Server-RDS-Learning-Path-54-Troubleshoot-RDS-DNS-and-Kerberos`
