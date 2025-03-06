---
icon: face-angry-horns
---

# D3m0n1z3dShell

D3m0n1z3dShell is an advanced tool designed to establish and maintain persistence on Linux systems. Developed by MatheuZSecurity, it offers various methods to ensure continued access to compromised machines.

**Key Features:**

* **SSH Keypair Generation:** Automatically generates SSH key pairs for all users, facilitating unauthorized access.
* **Persistence Mechanisms:**
  * _APT Persistence:_ Ensures the tool remains active through package management systems.
  * _Crontab Persistence:_ Utilizes scheduled tasks to maintain access.
  * _Systemd Persistence:_ Implements both user-level and root-level systemd services for persistence.
  * _Bashrc Persistence:_ Modifies user shell configurations to reload the tool upon terminal access.
* **Privilege Escalation:**
  * _Privileged User & SUID Bash:_ Creates privileged users and sets SUID on bash to escalate privileges.
  * _LD\_PRELOAD Setup:_ Employs dynamic linker/loader preloading for privilege escalation.
* **Rootkit Integration:**
  * _LKM Rootkit:_ Incorporates a Loadable Kernel Module rootkit, modified to bypass detection tools like rkhunter and chkrootkit.
  * _ICMP Backdoor:_ Implements a backdoor using ICMP packets for covert communication.
* **Static Binaries:** Provides tools for process monitoring, credential dumping, system enumeration, and more.

**Installation Methods:**

1.  **Standard Installation:**

    ```bash
    git clone https://github.com/MatheuZSecurity/D3m0n1z3dShell.git
    cd D3m0n1z3dShell
    chmod +x demonizedshell.sh
    sudo ./demonizedshell.sh
    ```
2.  **One-Liner Installation:**

    ```bash
    curl -L https://github.com/MatheuZSecurity/D3m0n1z3dShell/archive/main.tar.gz | tar xz
    cd D3m0n1z3dShell-main
    sudo ./demonizedshell.sh
    ```
3.  **Static Loading:**

    ```bash
    sudo curl -s https://raw.githubusercontent.com/MatheuZSecurity/D3m0n1z3dShell/main/static/demonizedshell_static.sh -o /tmp/demonizedshell_static.sh
    sudo bash /tmp/demonizedshell_static.sh
    ```

**Pending Features:**

* Development of an LD\_PRELOAD rootkit.
* Process injection capabilities.
* Additional persistence methods, including modifications to `rc.local`, `init.d`, and `motd`.
* Persistence via PHP and ASPX web shells.

**Disclaimer:** The use of D3m0n1z3dShell is intended for educational purposes only. Unauthorized use on systems without explicit permission is illegal and unethical.

**Contribution:** For contributions or inquiries, contact the developer on Twitter: [@MatheuzSecurity](https://twitter.com/MatheuzSecurity).

For more details and updates, visit the [GitHub repository](https://github.com/MatheuZSecurity/D3m0n1z3dShell).

