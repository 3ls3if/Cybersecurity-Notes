# LAPS

## Theory

### LAPS

Microsoft Local Administrator Password Solution (LAPS) is a free tool that helps manage passwords for local administrative accounts on Windows devices. LAPS stores passwords in Active Directory (AD) and automatically updates them regularly. LAPS also protects passwords with ACLs, which means that only eligible users can read or request a password reset.

### LAPS Toolkit

Functions written in PowerShell that leverage PowerView to audit and attack Active Directory environments that have deployed Microsoft's Local Administrator Password Solution (LAPS). It includes finding groups specifically delegated by sysadmins, finding users with "All Extended Rights" that can view passwords, and viewing all computers with LAPS enabled.



***

## REFERENCES

* [https://techcommunity.microsoft.com/t5/itops-talk-blog/step-by-step-guide-how-to-configure-microsoft-local/ba-p/2806185](https://techcommunity.microsoft.com/t5/itops-talk-blog/step-by-step-guide-how-to-configure-microsoft-local/ba-p/2806185)

