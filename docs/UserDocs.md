# PyCrucible User Docs

PyCrucible help you package and run your application without any prior setup. It essencailly speaking wrap or make a exe out of your python application. It help in deliver your application to your target user without them require to have any knowledge of python programming...

In this document, you will learn how can you package your application and make a kind of executable binary out of it..

## Prerequisite

- pycrucible cli program
- rust language (rustc, cargo)
- your source code (ofcourse, what else would you make executable out of!!)

you would need a pycrucible cli program that will help you package your app, and you will also need rust compiler for making a launcher.

you download PyCrucible CLIfrom [here](https://github.com/razorblade23/PyCrucible/releases)!! and Rust tools from [here](https://www.rust-lang.org/tools/install)!!

along, with you will require a source code of the application that you want to make in a executable.

> [!Note]
> Rust compiler & Cargo is a internal hidden dependency for the PyCrucible CLI.
> CLI App need rust tools for compile and generating launcher (a.k.a executable of your program).
> Just be sure to have them. and ensure that you can access them from anywhere.. mean your environment variables are set correctly...

## Steps (Complete Baby Step Guide)

Below given steps are for complete beginners. feel free to adjust or skip this steps if, you know what you are doing!!

1. Navigate your project folder (that you want to make executable of).

2. Check wether your project is compatible with Pycrucible.

   - check your project config with crucible expect config. if supports you are good to go.
   - else, you might need to put efforts in make it compatible

   > [!WARNING]
   > at present v0.1.4, current crucible only supports uv based projects...

> [!TIP]
> if you are not use vcs, and willing to trade off time for safety. then take extra step and make a copy of project directory on your desktop and use it instead of original project folder.

3. Download the pycrucible cli app and move it t project directory.

4. Now, if you are willing to customize the app. if not defualts are just fine.

   - create a `pycrucible.toml` and customize it.
   - you can copy the [template](https://github.com/razorblade23/PyCrucible/blob/main/pycrucible.toml.example) of it from your repository.

5. Now, run pycrucible cli program in project directory.

   ```bash
   pycrucible .
   ```

6. It might take time and might also take a lot of ram so wait.

7. Eventually, it will be over and you will be greeted with success message..

8. Now, open a path `~\payload\target\release` in File Manager.

9. You will see a exeutable called `pycrucible-launcher` launch it.

10. now move that to your download folder and check wether it run there, ideal it should work..
