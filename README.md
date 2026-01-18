# actor-IaC-examples

Example workflows for actor-IaC infrastructure automation.

[![Java Version](https://img.shields.io/badge/java-21+-blue.svg)](https://openjdk.java.net/)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)

## Overview

This repository contains example workflows demonstrating actor-IaC capabilities for infrastructure management and system information collection.

## Installation

### Prerequisites

First, install POJO-actor and actor-IaC to your local Maven repository:

```bash
# Install POJO-actor
git clone https://github.com/scivicslab/POJO-actor
cd POJO-actor
git checkout v2.12.1
mvn install

# Install actor-IaC
cd ..
git clone https://github.com/scivicslab/actor-IaC
cd actor-IaC
git checkout v2.12.1
mvn install
```

**Note:** Do not use `mvn clean install`. Use `mvn install` only. The `clean` target may cause issues due to the Maven repository configuration in pom.xml.

### Clone Examples

```bash
git clone https://github.com/scivicslab/actor-IaC-examples
cd actor-IaC-examples
git checkout v2.12.1
```

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
# Collect system info from compute nodes
./actor_iac.java run -d ./sysinfo -w main-collect-sysinfo -i inventory.ini -g compute

# Collect and analyze with plugin
./actor_iac.java run -d ./sysinfo -w main-collect-and-analyze -i inventory.ini -g compute
```

## Inventory Files

- **inventory.ini** - Example inventory with compute nodes
- **localhost.ini** - Local-only inventory for testing

## Plugins

The `plugins/` directory contains JAR files for workflow extensions:

- **actor-IaC-plugins-1.0.0.jar** - H2 database analyzer plugin for system info aggregation

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.
