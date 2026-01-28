# actor-IaC-examples

Example workflows for actor-IaC infrastructure automation.

[![Java Version](https://img.shields.io/badge/java-21+-blue.svg)](https://openjdk.java.net/)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)

## Overview

This repository contains example workflows demonstrating actor-IaC capabilities for infrastructure management and system information collection.


## Quick Start (No Cluster Required)

You can try actor-IaC on your local machine without any cluster setup.

### 1. Install Dependencies

```bash
# Install POJO-actor
git clone https://github.com/scivicslab/POJO-actor
cd POJO-actor
mvn install

# Install actor-IaC
cd ..
git clone https://github.com/scivicslab/actor-IaC
cd actor-IaC
mvn install
```

### 2. Clone Examples and Run

```bash
git clone https://github.com/scivicslab/actor-IaC-examples
cd actor-IaC-examples

# Run hello world example on localhost
./actor_iac.java run -d ./hello -w main-hello -i localhost.ini -g all
```

**Expected Output:**
```
[node-localhost] Hello from actor-IaC!

Workflow completed successfully
```

### 3. Collect System Info (Localhost)

```bash
./actor_iac.java run -d ./sysinfo -w main-collect-sysinfo -i localhost.ini -g all
```

This collects system information (hostname, CPU, memory, disk, network) from your local machine.


## Examples

### hello/

Simple "Hello World" workflow demonstrating basic actor-IaC usage.

```bash
./actor_iac.java run -d ./hello -w main-hello -i localhost.ini -g all
```

### sysinfo/

System information collection workflows:

- **main-collect-sysinfo.yaml** - Collect basic system info (hostname, OS, CPU, memory, disk, GPU, network)
- **main-collect-and-analyze.yaml** - Collect and analyze system info using H2 database plugin
- **main-collect-kvm-info.yaml** - Collect KVM/libvirt virtualization information
- **main-collect-microk8s-info.yaml** - Collect MicroK8s cluster information

```bash
# Collect system info from localhost
./actor_iac.java run -d ./sysinfo -w main-collect-sysinfo -i localhost.ini -g all

# Collect system info from compute nodes (requires cluster)
./actor_iac.java run -d ./sysinfo -w main-collect-sysinfo -i inventory.ini -g compute

# Collect and analyze with plugin
./actor_iac.java run -d ./sysinfo -w main-collect-and-analyze -i inventory.ini -g compute
```

### prereqs/

Prerequisite verification workflow:

```bash
./actor_iac.java run -d ./prereqs -w main-verify-prereqs -i localhost.ini -g all
```


## Inventory Files

- **localhost.ini** - Local-only inventory for testing (no SSH required)
- **inventory.ini** - Example inventory with compute nodes (SSH access required)

### Creating Your Own Inventory

For cluster usage, create an inventory file with your nodes:

```ini
[compute]
node1 ansible_host=192.168.1.101
node2 ansible_host=192.168.1.102
node3 ansible_host=192.168.1.103
```


## Plugins

The `plugins/` directory contains JAR files for workflow extensions:

- **log-analyzer-plugin-1.0.0.jar** - H2 database analyzer plugin for system info aggregation


## References

- [actor-IaC Documentation](https://scivicslab.com/docs/actor-iac/introduction)
- [actor-IaC GitHub](https://github.com/scivicslab/actor-IaC)
- [POJO-actor Tutorial](https://scivicslab.com/blog/2025-12-30-TutorialPart2-1)


## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.
