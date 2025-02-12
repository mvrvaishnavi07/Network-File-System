# Network-File-System

# Network File System (NFS) in C

## Introduction
The **Network File System (NFS)** is a distributed file system architecture that enables clients to interact with files stored on remote servers seamlessly. This implementation consists of three primary components:

1. **Clients:** Systems or users requesting file operations (e.g., read, write, delete, stream) within the NFS.
2. **Naming Server (NM):** A central hub coordinating client and server communications by locating the appropriate storage server for requested files or folders.
3. **Storage Servers (SS):** Servers managing the physical storage and retrieval of files and directories, ensuring data persistence and accessibility.

## Key Features
### File Operations Supported:
- **Writing a File/Folder:** Create and update content within the NFS, including synchronous and asynchronous writes.
- **Reading a File:** Retrieve the contents of files stored in the NFS.
- **Deleting a File/Folder:** Remove files or directories to manage storage efficiently.
- **Creating a File/Folder:** Generate new files and directories within the system.
- **Listing All Files and Folders:** Navigate the file structure and retrieve directory contents.
- **Getting File Metadata:** Access file details such as size, permissions, and timestamps.
- **Streaming Audio Files:** Stream audio directly from the NFS.

## System Architecture and Specifications

### 1. Naming Server (NM) and Storage Servers (SS)
#### 1.1 Initialization
- **Naming Server Initialization:** 
  - Manages directory structure and file locations.
  - Registers with clients and storage servers dynamically, handling non-hardcoded IPs and ports.
- **Storage Server Initialization:** 
  - Storage servers register with the Naming Server by providing their IP, port, and accessible paths.
  - Multiple storage servers can dynamically join the system during runtime.

#### 1.2 Storage Server Functionalities
- **Dynamic Addition of Servers:** 
  - New storage servers can register with the NM at any time.
- **Commands from NM:**
  - **Create Empty File/Directory:** Initialize a new file or folder.
  - **Delete File/Directory:** Remove specific data items.
  - **Copy Files/Directories:** Transfer data between servers using NM-provided addresses.
- **Client Interactions:**
  - Read and write operations.
  - Retrieve file size and permissions.
  - Stream audio files.

#### 1.3 Naming Server Functionalities
- **Central Repository:** Stores details about all connected storage servers and their accessible paths.
- **Client Feedback:** Provides clients with task status and server information for requested operations.

### 2. Client Functionalities
Clients interact with the Naming Server to perform various file-related tasks, such as:

- **Path Resolution:** 
  - E.g., `READ dir1/dir2/file.txt` triggers NM to locate the file and provide the correct SS details.
- **File/Folder Management:**
  - **Reading/Writing Files:** Access and modify file contents.
  - **Creating/Deleting Files:** Initialize or remove data items.
- **File Copying:** Transfer files or directories between SSs.
- **Listing Accessible Paths:** Retrieve all available paths for exploration.

### Example Commands
#### Example 1: Reading a File
```bash
Client: READ <path>
NS: IP: 10.2.141.242 Port: 5050
Client sends request to SS.
SS: "File content response."
```

#### Example 2: Streaming Audio
```bash
Client: STREAM <path>
NS: IP: 10.2.141.242 Port: 5050
Client sends request to SS.
SS sends audio packets to client for streaming.
```

#### Example 3: Creating a File
```bash
Client: CREATE <path> <name>
NS checks availability of path.
NS sends request to SS to create file.
SS: "Acknowledgment sent to NM."
NM: "Acknowledgment sent to client."
```

## Installation and Usage
### Prerequisites
- GCC compiler
- Network-enabled environment

### Steps to Run
1. Clone the repository:
   ```bash
   git clone <repository-link>
   ```
2. Compile the code:
   ```bash
   make
   ```
3. Start the Naming Server:
   ```bash
   ./naming_server
   ```
4. Initialize Storage Servers:
   ```bash
   ./storage_server <server_id> <config>
   ```
5. Run the Client:
   ```bash
   ./client
   ```

### Configuration Details
- IPs and ports must be dynamically assigned during runtime.
- Each SS should specify accessible paths during initialization.

## Additional Features
- **Asynchronous Writes:** Optimized performance for large files.
- **Dynamic Server Addition:** Scale storage dynamically.
- **File Metadata Retrieval:** Comprehensive insights into stored files.
- **Audio Streaming Support:** Stream directly to media players.

## Future Enhancements
- Add redundancy mechanisms for fault tolerance.
- Implement user authentication and access control.
