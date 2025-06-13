# CosmOS: A Secure Custom Operating System Kernel in Rust

Welcome to CosmOS - Custom Open-Source Modular Operating System, an ambitious journey into crafting a **custom operating system kernel** from the ground up, built with the power and safety of **Rust** for the **x86-64 architecture**. This project isn't just about putting code on silicon; it's about deeply understanding how an OS works, securing its very foundations, and pushing the boundaries of what's possible in a bare-metal environment.

---

## What's Under the Hood?

CosmOS is steadily evolving, piece by painstaking piece, to create a robust and reliable system. Here's a glimpse into the foundational work currently driving it:

* **Bare-Metal Beginnings**: We start from the ground up, setting up the critical **Global Descriptor Table (GDT)** and **Interrupt Descriptor Table (IDT)** to manage how the CPU operates and responds to events. This includes handling those tricky CPU exceptions, from unexpected page faults to critical double faults, ensuring the system remains stable.

* **Smart Memory Management**: Beyond just allocating space, CosmOS meticulously manages physical and virtual memory. This means a careful **frame allocator** to keep track of available physical pages and a **paging system** that intelligently maps virtual addresses to physical ones, keeping different parts of the system safely isolated. There's also a **kernel heap** for dynamic memory needs.

* **Bringing Hardware to Life**: We're talking to the metal! Our kernel includes drivers for essential input devices like the **VGA text mode** (so we can actually see what's happening!), the **PS/2 keyboard**, and the **PS/2 mouse**. We're also interfacing with the **VirtIO block device**, which is our primary way of communicating with a virtual disk for storage.

* **Making Things Move: Multitasking**: CosmOS orchestrates processes and threads, allowing multiple tasks to seemingly run at the same time. This involves meticulous **context switching** to smoothly transition between tasks and a **preemptive scheduler** that ensures everyone gets their fair share of CPU time.

* **Talking Behind the Scenes: IPC**: Threads and processes don't live in isolation. CosmOS implements basic **Inter-Process Communication (IPC)** mechanisms, like channels, allowing different parts of the kernel (and eventually user programs) to exchange messages and coordinate their work.

* **Userland's Gateway: System Calls**: The kernel exposes a carefully controlled set of **system calls**, acting as the secure gateway for user programs to request kernel services. This ensures that user applications can interact with the system without directly accessing privileged hardware or memory.

* **Building a Home for Data: The File System**: A fundamental piece of any OS! CosmOS is building a persistent file system from the ground up. This includes:

    * The **superblock**, holding vital metadata about the disk's layout.

    * **Inodes** to track file and directory properties.

    * **Directory structures** that map names to content.

    * A **block allocator** that intelligently manages disk space.

    * A **Virtual File System (VFS)** layer, designed to abstract away the specifics of different file system implementations, making it easier to integrate new ones down the line.

* **Bringing Programs to Life: ELF Loading**: We're implementing an **ELF loader** to parse and prepare executable programs for execution, mapping them into their own isolated memory spaces.

* **Peeking Inside: Hardware Info**: To help understand what's running underneath, CosmOS can now enumerate basic **PCI devices** and gather detailed information about the **CPU** and **memory configuration**.

* **Security, Always**: Every layer of CosmOS is being built with a sharp eye on security. From strict memory permissions and privilege separation to careful input validation in system calls, the goal is to create a kernel that is resilient against exploits and unauthorized access.

---

## Getting Started (for Developers)

If you're eager to poke around or contribute, here's what you'll need:

* **Rust Toolchain**: Make sure you have a `nightly` Rust toolchain installed, along with `rust-src` and `llvm-tools-preview` components.

* **QEMU**: A powerful open-source machine emulator, essential for running and testing CosmOS.

* **`just`**: A command runner (like `make`, but simpler) that automates common build and run tasks. Install it via `cargo install just`.

---

## How to Run CosmOS

1.  **Clone the Repository**:

    ```bash
    git clone [https://github.com/dotslashCosmic/cosmos.git](https://github.com/dotslashCosmic/cosmos.git)
    cd cosmos
    ```

2.  **Build and Run**:
    Simply use `just` from the project root:

    ```bash
    just
    ```

    This command will build the kernel and its bootloader, then launch it in QEMU. You'll see kernel messages appear in your terminal.

---

## Contributing

We'd love for you to join us on this adventure! Whether it's bug fixes, new features, documentation, or just feedback, all contributions are welcome. Feel free to open issues or pull requests.

---

Happy Hacking!
