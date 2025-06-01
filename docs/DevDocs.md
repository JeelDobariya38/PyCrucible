# Developer Guide to PyCrucible CLI

In this document, you will learn about the internal workings of the `PyCrucible CLI`. This guide outlines the flow and underlying logic of how the CLI transforms your Python application into a standalone executable.

## Overview

PyCrucible is a tool that runs a Python application using a UV binary. It extracts your package (as a ZIP file or directory), loads an optional configuration from `pycrucible.toml`, and uses `uv` to run your app in an ephemeral environment.

* **Input:** Your Python application source code.
* **Process:** A wrapping process handled by `uv`.
* **Output:** A standalone binary executable.

---

## Inner Flow & Magic

The **PyCrucible CLI Build Process** takes your source code and converts it into an executable through a series of steps:

### Build Process

1. Parse the command-line arguments using `clap`, producing a `CLI` struct:

   ```rs
   CLI {
       source_dir,
       uv_path,
       output_path,
       target
   }
   ```

2. Read the `pycrucible.toml` file into a `ProjectConfig` object (this contains project metadata and configuration).

3. Collect all source code files into a vector of `SourceFile { relative_path, content }`.

4. Check for the existence of a *manifest* file (e.g., `pyproject.toml`, `pylock.toml`, or `requirements.txt`) and determine its path.

5. Determine the `uv` binary path (involves some system checks—not critical to understand for the build process).

6. Construct a `BuilderConfig` object, which aggregates all build-related data:

   ```rs
   BuilderConfig {
       source_dir: File_Path,
       source_files: Vec<Source_File>,
       manifest: Content<Manifest_File>,
       uv_binary: Content<UV_Binary>,
       output_path: File_Path,
       cross: Option<String>
   }
   ```

7. Create a `LauncherGenerator` instance and pass in the `BuilderConfig`.

8. Begin compiling and generating the application launcher.

9. Collect all source files, zip them, and store them internally using the `zip` crate.

10. Convert the zipped source code into a byte array.

11. Convert the `uv` binary into a byte array.

12. At this point, both your source code and the UV binary are represented as byte arrays.

13. Create a new Cargo (Rust) project named `payload`. This Rust project is responsible for generating the launcher binary.

14. Copy a launcher template (`template.rs`) into the payload project and set it up for compilation.

15. Determine whether to compile for a cross-platform target or the native platform based on the `cross` field in `BuilderConfig`.

16. Compile the project using the Rust compiler, according to your platform preferences.

17. Copy the resulting binary to the specified output location.

18. Perform cleanup by deleting the temporary `payload` directory.

19. Done! Believe it or not.

20. Now, sit back, enjoy the success message, and—when ready—run the PyLauncher!
