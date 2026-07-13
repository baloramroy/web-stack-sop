## Standard Operating Procedure (SOP)
# Node.js Installation on Red Hat Enterprise Linux (RHEL) Using NodeSource Repository

## Document Information
| Attribute | Details |
|-----------|---------|
| **Title** | Node.js Installation on RHEL Using NodeSource Repository |
| **Version** | 1.0 |
| **Last Updated** | July 2026 |
| **Applies To** | Red Hat Enterprise Linux (RHEL) 7, 8, and 9 |
| **Installation Method** | NodeSource Repository |

---

## Pre-Installation Checks

- Verify RHEL Version
	```bash
	cat /etc/redhat-release
	# Example output: Red Hat Enterprise Linux release 9.2 (Plow)
	```

- Check Architecture
	```bash
	uname -m
	```

- Check for Existing Node.js Installation
	```bash
	which node
	node -v 2>/dev/null
	```

- Ensure System is Updated
	```bash
	dnf update   # RHEL 8/9
	# OR
	yum update   # RHEL 7
	```

- 1.5 Install Prerequisite Tools (If Needed)
	```bash
	dnf install -y curl wget tar gzip xz
	```
	>Install common tools needed across all methods

---

## Method A: NodeSource Repository Installation (Recommended)

**Best For:** Production environments needing up-to-date, maintainable installations with automatic security updates.

### Add NodeSource Repository

- Select the required Node.js major version.

	| Version | Command |
	|---------|---------|
	| Node.js 20.x (LTS) | `curl -fsSL https://rpm.nodesource.com/setup_20.x \| sudo bash -` |
	| Node.js 22.x (LTS) | `curl -fsSL https://rpm.nodesource.com/setup_22.x \| sudo bash -` |
	| Node.js 24.x (Current) | `curl -fsSL https://rpm.nodesource.com/setup_24.x \| sudo bash -` |

	> **Note:** Install the version recommended by your application vendor or organizational standard.

- Example:

	```bash
	curl -fsSL https://rpm.nodesource.com/setup_24.x | sudo bash -
	```

- **What this does:**
	- Adds NodeSource repository to `/etc/yum.repos.d/nodesource-el*.repo`
	- Imports NodeSource GPG key for package verification
	- Updates package cache

### Install Node.js

- For RHEL 8/9
	```bash
	dnf install nodejs
	```

- For RHEL 7 (if YUM is used)
	```bash
	yum install nodejs
	```

### Verify Installation

- Verify Node.js Version

	```bash
	node -v
	```

- Example:

	```text
	v24.18.0
	```

- Verify npm Version

	```bash
	npm -v
	```

- Verify npx Version

	```bash
	npx -v
	```

- Verify Corepack

	```bash
	corepack --version
	```


### Verify Global npm Package Location

- Run

  ```bash
  npm root -g
  ```

- Example

  ```text
  /usr/lib/node_modules
  ```


### Verify Installation Path

- Run

	```bash
	which node
	which npm
	which npx
	which corepack
	```

- Example

  ```text
  /usr/bin/node
  /usr/bin/npm
  /usr/bin/npx
  /usr/bin/corepack
  ```

---

## Functional Test

- Run:

	```bash
	node -e "console.log('Node.js installation successful')"
	```

- Expected output:

	```text
	Node.js installation successful
	```

---

## Uninstallation Procedures

### Uninstall Method A (NodeSource RPM)

- Remove Node.js
	```bash
	dnf remove nodejs
	```

- Disable NodeSource repository (optional)
	```bash
	dnf config-manager --disable nodesource
	```

- OR completely remove the repository
	```bash
	rm -f /etc/yum.repos.d/nodesource-el*.repo
	```

---


## Sign-off

| Role | Name | Date |
|------|------|------|
| **Prepared By** | Baloram Roy | 14-07-2026 |


---

**End of Document**