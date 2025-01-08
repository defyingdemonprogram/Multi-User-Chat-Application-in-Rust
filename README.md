## Basic Multi-User Chat Application

### Quick Start

1. **Build and Start the Server**
   Run the following commands to compile and launch the server:
   ```bash
   cargo build
   cargo run --bin server
   ```
   The generated authentication token will be stored in the `./TOKEN` file. The client will need this token to connect to the server.

2. **Connect to the Server**

   To start the client, execute:
   ```bash
   $ cargo run --bin client
   > /connect <server ip> <authentication token>
   ```
3. **Perform a Stress Test on the Server**

   To evaluate server performance under stress, use the following command:

   ```bash
   cargo run --bin pandora <attack_type> <ip>
   ```

   **Available Attack Types**:
   - **`dragon`**: Establishes connections and sends random data in bulk.  
   - **`hydra`**: Opens as many simultaneous connections as possible.  
   - **`gnome`**: Repeatedly opens and closes connections.  

   **Example**: To initiate the `hydra` attack on the server, run:  
   ```bash
   cargo run --bin pandora hydra 127.0.0.1:6969
   ```

   > **Deprecated Method**:
   > For a simpler, outdated approach to simulate load by sending multiple requests:  
   >```bash
   > cat /dev/urandom | nc 127.0.0.1 6969
   >```

#### Command for the Client
- `/connect <server ip> <token>`: Connects client to server
- `/disconnect`: Disconnect the clinet from server
- `/quit`: Quit the client
- `/help`: Print help


#### References
- [getrandom - GitHub Repository](https://github.com/rust-random/getrandom)
- [crossterm - GitHub Repository](https://github.com/crossterm-rs/crossterm)
- [rustls - Rustls Documentation](https://docs.rs/rustls/latest/rustls/)
- [mio - Github Repository](https://github.com/tokio-rs/mio)