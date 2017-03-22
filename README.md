# parity-tokio-ipc

This crate abstracts interprocess transport for UNIX/Windows. On UNIX it utilizes unix sockets (`tokio_uds` crate) and named pipe on windows (experimental `tokio-named-pipes` crate). 

Endpoint is transport-agnostic interface for incoming connections:
```rust
  let endpoint = match Endpoint::new(endpoint_addr, handle).unwrap();
  endpoint.for_each(|_| println!("Connection received!"));
```

And IpcStream is transport-agnostic io:
```rust
  let endpoint = match Endpoint::new(endpoint_addr, handle).unwrap();
  endpoint.for_each(|(ipc_stream: IpcStream, _)| io::write_all(ipc_stream, b"Hello!"));
```