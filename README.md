# containerd

[![Build Status](https://github.com/containerd/containerd/actions/workflows/ci.yml/badge.svg)](https://github.com/containerd/containerd/actions)
[![Go Report Card](https://goreportcard.com/badge/github.com/containerd/containerd)](https://goreportcard.com/report/github.com/containerd/containerd)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

A fork of [containerd/containerd](https://github.com/containerd/containerd) — an industry-standard container runtime with an emphasis on simplicity, robustness, and portability.

> **Personal fork** — used for learning and experimentation. For production use, see the [upstream project](https://github.com/containerd/containerd).

## Overview

containerd is available as a daemon for Linux and Windows. It manages the complete container lifecycle of its host system, from image transfer and storage to container execution and supervision to low-level storage to network attachments and beyond.

## Features

- **OCI Image Spec** support
- **OCI Runtime Spec** support (via runc and other OCI-compliant runtimes)
- **Image push and pull** support
- **Container lifecycle management** (create, start, stop, delete)
- **Network namespace management**
- **Multi-tenancy** via namespaces
- **Snapshotters** for various storage backends (overlayfs, btrfs, devmapper, etc.)
- **Content addressable storage**
- **gRPC API** for client integration
- **CRI plugin** for Kubernetes integration

## Getting Started

### Prerequisites

- Go 1.21 or later
- Linux kernel 4.x or later (for full feature support)
- `runc` or another OCI-compliant runtime

### Development Environment

This repository includes a [Dev Container](.devcontainer/) configuration for a consistent development environment.

1. Open in VS Code with the Dev Containers extension installed
2. Click **Reopen in Container** when prompted
3. The environment will be set up automatically

### Building from Source

```bash
# Clone the repository
git clone https://github.com/your-org/containerd.git
cd containerd

# Build the binaries
make build

# Run tests
make test

# Run a specific test package (useful during development)
go test ./snapshots/... -v

# Install binaries
sudo make install
```

### Running containerd

```bash
# Start containerd daemon
sudo containerd

# Use ctr CLI to interact
ctr images pull docker.io/library/ubuntu:22.04
ctr run docker.io/library/ubuntu:22.04 my-container
```

## Architecture

```
+-------------------------------+
|         containerd            |
|  +-------------------------+  |
|  |       gRPC API          |  |
|  +-------------------------+  |
|  |    Content Store        |  |
|  |    Snapshotter          |  |
|  |    Image Service        |  |
|  |    Container Service    |  |
|  |    Task Service         |  |
|  +-------------------------+  |
|  |      Runtimes (OCI)     |  |
|  +-------------------------+  |
+-------------------------------+
```

## Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md).
