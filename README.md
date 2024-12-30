## Basic Multi-User Chat Application

### Quick Start

1. **Build and Start the Server**
   Run the following commands to compile and launch the server:
   ```bash
   cargo build
   cargo run --bin server
   ```

2. **Connect to the Server**

   To start the client, execute:
   ```bash
   $ cargo run --bin client
   > /connect <server ip>
   > <authentication token>
   ```

   Alternatively, you can open two terminal windows and enter the following command in each:
   ```bash
   telnet 127.0.0.1 6969
   ```

3. **Perform a Stress Test on the Server**

   To simulate multiple requests for load testing, use:
   ```bash
   cat /dev/urandom | nc 127.0.0.1 6969
   ```

#### Command for the Client
- `/connect <server ip>`: Connects client to server

#### References
- [getrandom - GitHub Repository](https://github.com/rust-random/getrandom)
- [crossterm - GitHub Repository](https://github.com/crossterm-rs/crossterm)
- [rustls - Rustls Documentation](https://docs.rs/rustls/latest/rustls/)