# Podman

> [!NOTE]
> This document is written based on the `podman version 5.2.5` and has been tested.

## Installation

[Official docs](https://podman.io/docs/installation)

### Installing on Mac & Windows

> [!IMPORTANT]
> By default, Podman runs on a Linux machine. However, it also supports running on Windows and macOS (non-Linux machines) through a virtual machine called `podman machine`.
>
> The diagram below shows the Podman stack on a non-Linux machine.
> 
> ```
> +------------------------------------ + 
> | Non-Linux Host Machine (podman CLI) | 
> | +---------------------------------+ | 
> | | Podman Machine (Linux VM)       | | 
> | | +-----------------------------+ | |
> | | | Podman Runtime (runtime)    | | | 
> | | +-----------------------------+ | |
> | +---------------------------------+ |
> +-------------------------------------+
> ```
>
> If you try to execute a Podman command that requires the Podman runtime without a Podman machine, such as when executing `podman images`, the following error message will be shown.
> 
> ```
> Cannot connect to Podman. Please verify your connection to the Linux system using `podman system connection list`, or try `podman machine init` and `podman machine start` to manage a new Linux VM
> Error: unable to connect to Podman socket: failed to connect: dial tcp 127.0.0.1:63456: connect: connection refused
> ```
> 
> When installing Podman on a Windows or MAC machine, the installer will also install the `podman machine`.
> 
> ```
> podman machine --help
> ```
> 
> Before starting to use `podman`, it is first required to initialize a `podman machine`.
> 
> ```
> podman machine init --help
>
> # If the machine name is not specified, Podman creates the machine using the default settings.
> # This will create a Podman machine called "podman-machine-default".
> # This is sufficient most of the time.
> podman machine init
>
> # List all created machines
> podman machine info
> ```
> 
> Then, start the machine. Remember to start the machine after the host machine has restarted.
> 
> ```
> podman machine start --help
>
> # Podman will start the default machine if you don't specify the machine name
> podman machine start
> ```
>
> The machine can be stopped when it is no needed.
>
> ```
> podman machine stop
> ```

> [!IMPORTANT]
> For some custom and advanced use cases, it is required to change the `podman` configuration.
> These configurations need to be changed in the `podman machine`, not the host machine.
>
> To do this, use the `podman machine ssh` command to log in to the machine and make the necessary configuration changes.
> 
> ```
> podman machine ssh --help
> ```
> 
> For example, pushing images from the local environment to a custom registry (images hub) requires adding the custom registry endpoint in the `/etc/containers/registries.conf`.<sup>[\[1\]](https://podman-desktop.io/docs/containers/registries)</sup>
>
> So, the `/etc/containers/registries.conf` file is located in the `podman machine`.
>
> ```
> podman machine ssh
> sudo nano /etc/containers/registries.conf
>
> # After editing successfully, exit and restart the Podman machine.
> exit
> podman machine stop
> podman machine start
> ```

### MAC

Although it is not recommended to install via `brew`, it has been tested and works. The Podman Desktop is not necessary.

```
brew install podman
podman machine init
podman machine start
```
