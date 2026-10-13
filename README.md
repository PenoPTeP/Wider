# WiderOS

A GNU/Linux distro experiment with the goal of being user-friendly, easy to hack and customize, immutable, and modular. Usually, you only get one or two.
The goal is a system that's easy to use day to day but doesn't get in the way when you want to change how it works.

## Stack

- **Linux** — kernel and hardware support
- **Nix flakes** — building and packaging
- **OverlayFS** — immutable filesystem layers with writable overlays
- **Podman** — container runtime for system services
- **runit** — current service supervisor

The system is designed so that components can be replaced without tying the whole setup to one particular implementation.

## Init system

runit is the current choice for service supervision, but the service management layer is intended to be independent of the init system.

The aim is to make it possible to switch to something like s6 or dinit or even systemd without having to touch anything else at all.

## System services

System services are managed as part of the modular system, with Podman providing their runtime environment.

The setup includes system infrastructure such as D-Bus, device management, networking, login and session management, and time synchronization. These services need to integrate with the host, so their access to devices, sockets, and runtime directories is configured explicitly.

D-Bus provides system-wide IPC, while services that depend on it can be managed and updated separately. The same approach applies to other parts of the system.

## Filesystems and state

Software is separated from persistent data. OverlayFS provides a writable view over read-only module filesystems, while configuration and service state can live outside those filesystems.

This makes it easier to update or replace software without treating the entire system as one mutable installation.

## Development

The project is experimental and still under development. The module management, init abstraction, and system integration are evolving.

The focus is on making the system practical to use, straightforward to customize, and easy to work on without giving up immutability or modularity.
