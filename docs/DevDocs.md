# Developer Guide To PyCrucible CLI

In this document, You will learn about the internal details of `PyCrucible CLI`. Here, we you will find the flow and internal logic of the Pycrucible CLI.

## Overview

This tool runs a Python application with a help of UV binary. It extracts your package (ZIP or directory), loads an optional configuration from pycrucible.toml, and uses uv to run your app in an ephemeral environment.

- **Input:** your python application source code.
- **Process:** wrapping process that is done using uv.
- **Output:** a binary executable.

## Inner Flow & Magic

**PyCruible CLI Building Process** takes your source code and convert your app in executable in series of step.

### Building Process

1. Read the commandline arguments, as `CLI { source_dir, uv_path, output_path, target }`, underlying process is handle by `clap`.

2. Then, Read the pycruible.toml as `ProjectConfig { ... }` (it contains info of project).

3. Then, starts collecting your projects source code files as `Vector of SourceFile { relative_path, content }`.

4. Then, we check wether the 'manifest' file exist or not & get its path.
     - manifest file mean pyproject.toml/pylock.toml/requirements.txt

5. Then, get the uv path using some complicated process & some software check, that not important of building process.

6. Now, The real rocess starts, The program build instance of something called `BuilderConfig`.
   
   ```rs
   BuilderConfig {
       source_dir: File_Path,
       source_files: Vector<Source_File>,
       manifest: Content<Manifest_File>,
       uv_binary: Content<UV_Binary>,
       output_path: File_Path,
       cross: Optional<String>
    };
   ```

7. Then, It make a instance of `LauncherGenerator` and pass this `BuilderConfig` in it.

8. Then, starts compileing and generateing the app launcher...

9. It first, collect all your source code and zip it up.. and write that all in a zip fie internal object.. using `zip`.

10. Then, generate the byte array out of the zipped data. meaning, the zip file content is converted into byte array.

11. Then, generate the byte array out of the uv binary, meaning uv binary is conevrt as byte array.

12. Here By, we have both uv binary and your source code. both, are now there as a byte array mean, we both thing represented as byte array.

13. Now, we just make new cargo project in your source code. we call project "payload", the rust project is responsible for create a launcher.

14. The PyCrucible CLI copy the code, from the template.rs into the payload project. and setup and make the project ready for compile..

15. Now, atlast check wether you want to compile for cross platform or for native using the cross in builderconfig.

16. Then, it compile accoring to your preference, using rust compiler.

17. Then, it copy the output to desire location.

18. Take a clean up step and delete the payload directory.

19. And We are done believe me or not.

20. Now, Enjoy stare-ing at success message for hrs!! and when you are satified run the pylauncher!!
