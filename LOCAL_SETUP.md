# Local setup

## Prerequisites
Use Linux, or a Linux environment under WSL, with `g++`, GNU Make and POSIX pthread support. The source targets POSIX sockets and is not a native Windows application.

## Build
From the repository root:
```sh
make all
```
Individual targets are `make server` and `make client`.

## Safe local demonstration
Use only disposable sample data. The client can replace files with matching names. Run the client from a separate, empty output directory and do not point it at important data.

Server syntax:
```sh
./Data_Server/dataServer -p 9090 -s 4 -q 16 -b 4096
```

In another terminal, change into your disposable client output directory and run the client binary using its absolute path:
```sh
/path/to/repository/Remote_Client/remoteClient -i 127.0.0.1 -p 9090 -d sample-data
```

`sample-data` must be an existing directory relative to the server's working directory. Populate it with small, non-sensitive fixtures before starting the demo. Keep client output separate from the server's source tree. Server options: `-p` port, `-s` worker pool size, `-q` queue capacity and `-b` block size.

## Verification
Compare the received tree and file hashes to the original fixtures. Repeat with two clients, nested folders and empty files. Treat this as a manual integration check; there is no full automated protocol test suite in the original code.

## Troubleshooting
- Missing pthread/socket headers: build inside Linux/WSL.
- Port already in use: choose another non-privileged port on both ends.
- Missing directory: verify the server's current working directory.
- Unexpected overwrite: stop and move the demo to disposable directories.
- Large or malformed transfers need additional protocol/error-handling testing.

Do not expose the server directly to the internet.
