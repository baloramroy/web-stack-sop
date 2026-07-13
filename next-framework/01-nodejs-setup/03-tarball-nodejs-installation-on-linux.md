## Standard Operating Procedure (SOP)
# Node.js Installation on Red Hat Enterprise Linux (RHEL) Using Binary Tarball

## Document Information
| Attribute | Details |
|-----------|---------|
| **Title** | Node.js Installation on RHEL Using Binary Tarball |
| **Version** | 1.0 |
| **Last Updated** | July 2026 |
| **Applies To** | Red Hat Enterprise Linux (RHEL) 7, 8, and 9 |
| **Installation Method** | Binary Tarball |
| **Installation Scope** | System-wide |
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

## Method B: Tarball (Binary Archive) Installation

**Best For:** Development environments, testing, or when you need absolute control over installation location.

### Create a Working Directory

- Create a `nodejs` directory in the user home directory
  
	```bash
	sudo mkdir -p ~/nodejs && cd ~/nodejs
	```

### Download Binary Tarball

#### Option 1: Download a Specific Version

* Define the Node.js version and architecture.
	```bash
	NODE_VERSION="24.18.0"
	ARCH="x64"
	```

* Download the binary archive.

	```bash
	curl -LO https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-${ARCH}.tar.xz
	```


#### Option 2: Navigate and Download Manually

- Browse available versions and Download from browser:
	```
	https://nodejs.org/dist/
	```

- Or download directly using `wget`.

	```bash
	wget https://nodejs.org/dist/v24.18.0/node-v24.18.0-linux-x64.tar.xz
	```

### Verify SHA256 Checksum

- Download the official checksum file.

	```bash
	NODE_VERSION="24.18.0"
	ARCH="x64"

	curl -LO https://nodejs.org/dist/v${NODE_VERSION}/SHASUMS256.txt
	```

- Verify the downloaded archive.

	```bash
	grep "node-v${NODE_VERSION}-linux-${ARCH}.tar.xz" SHASUMS256.txt | sha256sum -c
	```

- Expected output:

	```text
	node-v24.18.0-linux-x64.tar.xz: OK
	```


### Extract Tarball

- Extract the archive into the working directory.

	```bash
	tar -xf node-v24.18.0-linux-x64.tar.xz --no-same-owner --no-same-permissions
	mv node-v24.18.0-linux-x64 node-v24.18.0
	```

- Directory structure becomes:

	```text
	~/nodejs/

	├── node-v24.18.0
	│   ├── bin
	│   ├── include
	│   ├── lib
	│   ├── share
	│   └── ...
	├── node-v24.18.0-linux-x64.tar.xz
	└── SHASUMS256.txt
	```

- Review the Extracted Files (Optional)

	```bash
	tree -L 2 node-v24.18.0
	```

---

## Install Node.js

### Create Installation Directory

- Create a dedicated installation directory under `/opt`.

	```bash
	sudo mkdir -p /opt/nodejs
	```

- Copy the extracted Node.js directory.

	```bash
	sudo cp -a node-v24.18.0 /opt/nodejs/
	```

- Directory structure becomes:

	```text
	/opt/nodejs/

	└── node-v24.18.0
			├── bin
			├── include
			├── lib
			├── share
			└── ...
	```

#

### Create a Standard Symlink

- Create a symbolic link named **current** that points to the installed version.

	```bash
	sudo ln -sfn /opt/nodejs/node-v24.18.0 /opt/nodejs/current
	```

- Verify:

	```bash
	ls -l /opt/nodejs
	```

- Example:

	```text
	current -> /opt/nodejs/node-v24.18.0
	node-v24.18.0
	```

#

### Create Executable Symlinks

- Expose the Node.js executables through `/usr/local/bin`.

	```bash
	sudo ln -sfn /opt/nodejs/current/bin/node /usr/local/bin/node
	sudo ln -sfn /opt/nodejs/current/bin/npm /usr/local/bin/npm
	sudo ln -sfn /opt/nodejs/current/bin/npx /usr/local/bin/npx
	sudo ln -sfn /opt/nodejs/current/bin/corepack /usr/local/bin/corepack
	```

#

### Verify Symbolic Links

- Run

  ```bash
  ls -l /usr/local/bin/node
  ls -l /usr/local/bin/npm
  ls -l /usr/local/bin/npx
  ls -l /usr/local/bin/corepack
  ```

- Example:

  ```text
  node -> /opt/nodejs/current/bin/node
  npm -> /opt/nodejs/current/bin/npm
  npx -> /opt/nodejs/current/bin/npx
  corepack -> /opt/nodejs/current/bin/corepack
  ```

---

## Post-Installation Verification

### Verify Installation Version

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

### Verify Installation Path

- Ensure `/usr/local/bin` exists in the system PATH.

	```bash
	echo $PATH
	```

- Example:

	```text
	/root/.local/bin:/root/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin
	```


- Run

	```bash
	which node
	which npm
	which npx
	which corepack
	```

- Expected output:

	```text
	/usr/local/bin/node
	/usr/local/bin/npm
	/usr/local/bin/npx
	/usr/local/bin/corepack
	```

### Verify Symlink Targets

- Run:

	```bash
	readlink -f $(which node)
	readlink -f $(which npm)
	readlink -f $(which npx)
	```

- Expected output:

	```text
	/opt/nodejs/node-v24.18.0/bin/node
	/opt/nodejs/node-v24.18.0/bin/npm
	/opt/nodejs/node-v24.18.0/bin/npx
	```

### Verify Global npm Package Location

- Run:

	```bash
	npm root -g
	```

- Example:

	```text
	/opt/nodejs/current/lib/node_modules
	```
---

## Functional Test

- Execute a simple JavaScript program.

```bash
node -e "console.log('Node.js installation successful')"
```

Expected output

```text
Node.js installation successful
```

---

## Upgrade Procedure

**Purpose:** Upgrade Node.js to a newer version while preserving the existing installation for easy rollback.

### Download the New Version

- Define the new Node.js version.

	```bash
	NODE_VERSION="24.19.1"
	ARCH="x64"
	```

- Download the binary archive.

	```bash
	curl -LO https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-${ARCH}.tar.xz
	```

- Download the checksum file.

	```bash
	curl -LO https://nodejs.org/dist/v${NODE_VERSION}/SHASUMS256.txt
	```

- Verify the archive.

	```bash
	grep "node-v${NODE_VERSION}-linux-${ARCH}.tar.xz" SHASUMS256.txt | sha256sum -c
	```

-	Expected output:

	```text
	node-v24.19.1-linux-x64.tar.xz: OK
	```

#

### Extract the Archive

- Run:

	```bash
	tar -xf node-v24.19.1-linux-x64.tar.xz --no-same-owner --no-same-permissions
	```

- Rename it like this:

	```bash
	mv node-v24.19.1-linux-x64 node-v24.19.1
	```

#

### Install the New Version

- Copy the new version into the installation directory.

	```bash
	sudo cp -a node-v24.19.1 /opt/nodejs/
	```

- Directory structure becomes:

	```text
	/opt/nodejs/

	├── current -> /opt/nodejs/node-v24.18.0
	├── node-v24.18.0
	└── node-v24.19.1
	```

#

### Switch to the New Version

- Update the **current** symbolic link.

	```bash
	sudo ln -sfn /opt/nodejs/node-v24.19.1 /opt/nodejs/current
	```

---

### Verify the Upgrade

- Verify the active version.

	```bash
	node -v
	npm -v
	```

- Expected output:

	```text
	v24.19.1
	```

- Verify the symbolic link.

	```bash
	readlink -f $(which node)
	```

- Expected output:

	```text
	/opt/nodejs/node-v24.19.1/bin/node
	```

#

### Remove the Previous Version (Optional)

- After confirming the new version is operating correctly, remove the old installation if it is no longer required.

	```bash
	sudo rm -rf /opt/nodejs/node-v24.18.0
	```

	> **Note**\
	> Retaining the previous version is recommended until the upgraded application has been fully tested.

---

## Rollback Procedure

**Purpose:** Restore the previous Node.js version if an upgrade causes application or compatibility issues.

### Verify Available Versions

- List the installed Node.js versions.

	```bash
	ls -l /opt/nodejs
	```

- Example:

	```text
	current -> /opt/nodejs/node-v24.19.1
	node-v24.18.0
	node-v24.19.1
	```

#

### Switch Back to the Previous Version

- Update the **current** symbolic link.

	```bash
	sudo ln -sfn /opt/nodejs/node-v24.18.0 /opt/nodejs/current
	```

#

### Verify the Rollback

- Check the active version.

	```bash
	node -v
	```

- Expected output:

	```text
	v24.18.0
	```

- Verify the executable path.

	```bash
	readlink -f $(which node)
	```

- Expected output:

	```text
	/opt/nodejs/node-v24.18.0/bin/node
	```

#

### Remove the Failed Version (Optional)

- If the upgraded version is no longer required, remove it after confirming the rollback is successful.

	```bash
	sudo rm -rf /opt/nodejs/node-v24.19.1
	```

	> **Note**
	>
	> Only remove the newer version after confirming that all applications are functioning correctly with the restored version.

---

## Uninstallation Procedure

- Remove Symbolic Links

	```bash
	sudo rm -f /usr/local/bin/node
	sudo rm -f /usr/local/bin/npm
	sudo rm -f /usr/local/bin/npx
	sudo rm -f /usr/local/bin/corepack
	```

- Remove Node.js Installation

	```bash
	sudo rm -rf /opt/nodejs
	```

- Verify Removal

	```bash
	which node
	which npm
	which npx
	```

- Expected output

	```text
	node: no node in (...)
	```

---