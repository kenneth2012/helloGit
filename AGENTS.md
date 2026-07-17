# AGENTS.md

Guidance for AI agents working in this repository.

## Project overview

`helloGit` is a minimal Eclipse-style Java project with a single entry class, `HelloJava`, under `src/`. There is no Maven, Gradle, or package manager; the JDK on the machine is the only toolchain dependency.

## Cursor Cloud specific instructions

- **JDK**: OpenJDK 21+ on the VM is sufficient. Eclipse metadata targets Java SE 1.6; modern `javac` compiles this source without changes.
- **No long-running services**: Nothing listens on a port. Validation is compile-and-run only.
- **Build output**: Compiled classes go to `bin/` (gitignored). Create it before compiling if missing: `mkdir -p bin`.
- **Compile and run** (from repo root):

  ```bash
  javac -d bin src/HelloJava.java
  java -cp bin HelloJava
  ```

  `main` is currently empty, so a successful run exits with code `0` and produces no console output.
- **Lint / tests**: No ESLint, Checkstyle config, or test suite in the repo. There is nothing to run beyond `javac` and `java`.
- **Eclipse (optional)**: Import `/workspace` as an existing project using `.project` and `.classpath` if GUI workflow is needed.
