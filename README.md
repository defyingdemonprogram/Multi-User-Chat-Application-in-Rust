## Basic Multi-User Chat Application

### Quick Start

1. **Compile and Launch the Program**
   ```bash
   cargo build
   cargo run
   ```

2. **Establish a Server Connection**
   Open two terminal windows and run the following command in each:
   ```bash
   telnet 127.0.0.1 6969
   ```

3. **Perform a Stress Test on the Server**
   Use the following command to simulate multiple requests:
   ```bash
   cat /dev/urandom | nc 127.0.0.1 6969
   ```

#### References
- [getrandom - Github Repo](https://github.com/rust-random/getrandom)
- [rustls - Rustls Documentation](https://docs.rs/rustls/latest/rustls/)