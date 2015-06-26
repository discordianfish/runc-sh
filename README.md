# runc-sh
*Executable, self-contained containers with runc*

The `pack` script takes a Docker image and converts it to a single,
executable file.

# Usage

```
./pack ghost -o my-ghost-container
```

This command will:
- Create a temporary container from the image 'ghost'
- Exports the container filesystem
- Gets the images configuration (entrypoint etc)
- Merges this into a executable file `my-ghost-container`

When running the executable, it will extract the image to a
temporary directory and use runc to start a container. After the
container exited, it will remove the temporary files.

For now, the container uses host networking.

## Bind-mounts
You can specify bind mounts via `-v source[:destination]`. Where
`destination` defaults to `source` if omitted.

This converts [/frazelle]'s VLC image to a standalone executable:

```
./pack -o vlc -v /tmp/.X11-unix -v /var/run/user -v /dev/shm jess/vlc

```
