# PyCrucible User Docs

**PyCrucible** helps you package and run your Python application without any prior setup on the user's system. Essentially, it wraps your application into a standalone executable. This allows you to deliver your application to users—even if they have no knowledge of Python or haven’t installed Python on their system.

In this document, you'll learn how to package your application and turn it into a self-contained binary executable.

---

## Prerequisites

Before you begin, ensure you have the following:

* **PyCrucible CLI program**
* **Rust toolchain (rustc, cargo)**
* **Your Python source code** (obviously, you need something to make into an executable!)

You can download the required tools from:

* ✅ PyCrucible CLI: [Download from GitHub Releases](https://github.com/razorblade23/PyCrucible/releases)
* ✅ Rust (Compiler & Cargo): [Install from Rust Lang](https://www.rust-lang.org/tools/install)

Also, make sure you have the source code for the Python application you'd like to convert into an executable.

> \[!NOTE]
> The Rust compiler and Cargo are internal dependencies of PyCrucible CLI.
> They are required to compile the launcher (the executable wrapper for your app).
> Ensure Rust tools are installed and accessible from your terminal (i.e., environment variables are correctly set).

---

## Step-by-Step Guide (Beginner-Friendly)

The following steps are designed for users who are new to the process. If you're already experienced, feel free to skip or modify as needed.

---

### 1. Navigate to Your Project Folder

Go to the directory of the Python project you want to convert into an executable.

---

### 2. Check PyCrucible Compatibility

* Review your project configuration to ensure it's compatible with what PyCrucible expects.
* If it’s not directly supported, you may need to make a few adjustments to align with supported formats.

> \[!WARNING]
> As of version **v0.1.4**, PyCrucible currently supports only **UV-based** Python projects.

> \[!TIP]
> If you're not using version control and want to be cautious, make a copy of your project folder and work on that version to avoid any unwanted changes to your original files.

---

### 3. Download and Move PyCrucible CLI to Your Project Folder

Place the downloaded `pycrucible` executable in the root of your project directory.

---

### 4. (Optional) Customize with `pycrucible.toml`

If you want to customize the behavior of the packaging process:

* Create a `pycrucible.toml` configuration file.
* You can copy the [template config file](https://github.com/razorblade23/PyCrucible/blob/main/pycrucible.toml.example) from the repository and modify it as needed.

> If you skip this, the CLI will use default settings.

---

### 5. Run PyCrucible

From your terminal, execute the CLI tool in your project directory:

```bash
pycrucible .
```

This will initiate the build process.

---

### 6. Wait Patiently

The process may take a while and could use a significant amount of RAM—especially on large projects. Let it finish.

---

### 7. Success!

Eventually, the process will complete, and you’ll see a success message.

---

### 8. Locate the Executable

Navigate to:

```
<your project folder>/payload/target/release
```

You will find an executable file named something like:

```
pycrucible-launcher
```

---

### 9. Run the Executable

Launch it and see if it works!

---

### 10. Optional: Test Portability

Move the executable to a different folder (e.g., your Downloads directory) and try running it from there. Ideally, it should work just fine.
