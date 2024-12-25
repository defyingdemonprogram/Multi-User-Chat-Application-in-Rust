## Basic Multi-User Chat Application

### Quick Start

1. **Build and Start the Server**
   ```bash
   cargo build
   cargo run --bin server
   ```

2. **Connect to the Server**
   Open two terminal windows and execute the following command in each:
   ```bash
   telnet 127.0.0.1 6969
   ```
   Alternatively, you can start the client with:
   ```bash
   cargo run --bin client 127.0.0.1
   ```

3. **Perform a Stress Test on the Server**
   Use the following command to simulate multiple requests:
   ```bash
   cat /dev/urandom | nc 127.0.0.1 6969
   ```

#### References
- [getrandom - Github Repo](https://github.com/rust-random/getrandom)
- [crossterm - Github Repo](https://github.com/crossterm-rs/crossterm)
- [rustls - Rustls Documentation](https://docs.rs/rustls/latest/rustls/)