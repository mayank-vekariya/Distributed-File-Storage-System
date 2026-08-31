# Architecture

![Transfer flow](docs/assets/architecture.svg)

## Server
`Data_Server/dataServer.cpp` initializes the listener and shared state. Communication threads receive directory requests. Recursive traversal submits file jobs to a bounded queue. Worker threads wait on synchronization primitives and consume the queued jobs.

`Data_Server/helperFunctions.cpp` contains the thread and transfer helpers. Per-socket mutexes prevent multiple workers from interleaving a file's protocol messages on a single client connection.

## Client
`Remote_Client/remoteClient.cpp` connects, requests a directory, receives path/metadata/content and reconstructs the directory hierarchy locally.

## What this demonstrates
- Backpressure through a bounded producer/consumer queue.
- Thread synchronization and serialized access to each socket.
- Separation of connection handling from file-transfer work.
- Low-level file and network I/O.

## What it does not promise
TCP provides an ordered byte stream, not an application-level message protocol or automatic whole-file validation. This prototype is not a replicated storage cluster, encrypted transfer service or hardened file server. It has no authentication/TLS. Review path containment, malformed input, short reads/writes, cancellation and resource cleanup before extending it.

## Original reference visual
The original README's [server/client diagram](https://user-images.githubusercontent.com/73662635/180067338-e6df7da1-c5e4-4f0c-89e2-a787c2d01608.png) is retained here as a reference. The new diagram documents the same communication-thread / queue / worker-pool separation.
