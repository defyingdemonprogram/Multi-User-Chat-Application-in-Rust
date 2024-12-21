## Basic Multi-User Chat Application

### Setting Up

1. **Compile and Launch the Program**
   ```bash
   rustc -o server server.rs
   ./server
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