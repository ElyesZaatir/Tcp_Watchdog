Process Connection Watchdog (Rust)

This Rust program acts as a process watchdog and connection monitor. It continuously checks if a specified process is running and maintains an active connection to a given IP address. If either the process is missing or the connection is lost, the program will kill and restart it.

    ⚠️ Most actual values (like IPs and process names) have been removed for authenticity.

⚙️ Features

    Monitors a process by name using the sysinfo crate.

    Checks for active TCP connections using netstat.

    Restarts the process if it isn't running or if a connection to a specific IP is missing.

    Hosts a basic TCP server that logs incoming messages.

    Graceful error handling with user prompts and shutdown delay.

🛠️ Requirements

    Rust (1.65+ recommended)

    Windows OS (due to use of taskkill and netstat)

    Admin privileges might be needed to kill/restart certain processes

Install dependencies and build:

cargo build --release

🚀 Usage

    Update the following variables in main.rs:

        process_name – name of the target executable (e.g., "Process.exe")

        desired_ip – IP address the process should stay connected to

        start_tcp_server("") – replace "" with the desired bind address like "127.0.0.1:8080" if needed

    Run the compiled binary:

cargo run --release

🧪 What It Does

    Checks every 25 seconds if:

        The process is running.

        There’s a connection to the specified IP using the process’s PID.

    If not connected:

        Kills the process using taskkill /F /PID <pid>

        Restarts the process by name (Command::new(process_name).spawn())

    Runs a TCP server to log messages from incoming connections.

💡 Example Output

Process MyApp.exe is running (PID: 1234).
No active connection to 192.168.1.100. Killing and restarting process...
Successfully restarted the process.
TCP server listening
New connection: 127.0.0.1:55000
Received: ping

📌 Notes

    The script assumes netstat -ano works in your environment. You may need to adapt for cross-platform support.

    taskkill is specific to Windows; for Unix systems, use kill.

    The TCP server is optional but useful for diagnostics or external control.

🔐 Legal & Safety Disclaimer

This tool is intended for educational and internal use only. Automatically managing or restarting processes should be done with care. Ensure it does not violate system policies or service agreements.
