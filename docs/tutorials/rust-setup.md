# Setting up a dev container for Rust

* Primary author: [Kaw Bu](https://github.com/kawbu)
* Reviewer: [Kamal Deep Vasireddy](https://github.com/Kamal135792)


## Prerequisites

Before we dive in, make sure you have:

1. **A [GitHub](https://www.github.com) account** 
2. **[Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) already installed**
3. **[Visual Studio Code](https://code.visualstudio.com/)**
4. **[Docker preinstalled](https://www.docker.com/products/docker-desktop)**
5. **COMP211** Credit

## Project Setup

### Create a Local Directory and Initialize Git

(A) Open your terminal/command prompt.  
(B) Create a new directory for your project.

```
mkdir rust-tutorial
cd rust-tutorial
```

(C) Initialize a new Git repo:

```
git init
```

!!! danger "What is the effect of running the `init` subcommand?"
    **You should know what this does already**

(D) Create a README file:

```
echo "# Rust Tutorial" > README.md
git add README.md
git commit -m "Initial commit with README"
```

### Create a Remote Repo on GitHub

(1) Log into your GitHub account and find the [Create a New Repository](https://github.com/new) page.  
(2) Fill in these following details:

- **Repository Name:** `rust-tutorial`
- **Description:** "Introductory project to the Rust programming language"
- **Visibility:** Public  

(3) **Do not initialize the repository with a README, .gitignore, or license.**  
(4) Click **Create Repository**

### Link your Local Repo to GitHub

(1) Add the GitHub repository as a remote:
`git remote add origin https://github.com/<bob-ross>/rust-tutorial.git`  
Replace `<bob-ross>` with your GitHub username.  

(2) Ensure your default branch name is `main` with the subcommand `git branch`. Rename it to `main` with the following command: `git branch -M main` if necessary.  

(3) Push local commits to the GitHub repository:
`git push --set-upstream origin main`  
!!! tip "Purpose of the '--set-upstream' Flag"
    The command `git push --set upstream origin main` pushes the main branch to the remote repository origin. The flag serves to set up the main branch to track the remote branch, so that further pushes/pulls with/to that branch can be done without specifying the branch name and simply just writing `git push origin` will suffice when work is done on the local `main` branch.  

(4) When refreshing your GitHub repository, you will now see that the same commit that was created locally has now been *pushed* to remote. The command `git log` can be used locally to see the commit ID and message, which should match the ID of the most recent commit on GitHub. This is a result of the previous step!

## Setting up the Development Environment

### Add Development Container Configuration

1. In VS Code, open the `rust-tutorial` directory.
2. (If you havent already) Install the **Dev Containers** extension for VS Code
3. Create a `.devcontainer` directory in the root of your project.  
4. Create a `devcontainer.json` file within the `.devcontainer` directory, with the following code:

```json
{
  "name": "Rust Tutorial",
  "image": "mcr.microsoft.com/devcontainers/rust:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["rust-lang.rust-analyzer"]
    }
  }
}
```

The `devcontainer.json` file defines the configuration for your development environment. In this case, we're specifying the following:

-`name`: A descriptive name for the container.  
-`image`: The docker image to use.  
-`customizations`: Adds useful configurations to VS Code.  

## Opening the Project in a Dev Container

1. In VS Code, open the container by pressing `Ctrl+Shift+P`, and select the option which says "Dev Containers: Reopen in Container".

!!! warning "Troubleshooting `Dev Containers: Reopen in Container`"
    Ensure you are inside of the rust-tutorial directory when running this command! Otherwise VS Code will prompt you to provide a container build, as it cannot detect the `.devcontainer` directory and `devcontainer.json` file!  

2. Now, your dev container is set up! Close the current terminal tab, and open a new one.
3. To ensure that rust is running, run the command `rustc --verison` and ensure no errors appear. This should also show you the latest version of Rust which has just been installed on your working container.

!!! success "Output of `rustc --version`"
    After creating your container and running `rustc --version`, you may see that your version of Rust differs from if you were to create your container a month or two ago! This is because programming languages are always receiving updates and changes!

## Writing your first Rust Program

### What is Rust?

Rust is a fast and efficient programming language published on May 15, 2015. It is widely used for the creation of low-level projects, such as Operating Systems. It is favored by many people for multiple reasons, such as:

- Efficient Stack/Heap Storage
- Many Safety Features
- A Strong Ecosystem

### Creating a Rust Project File

Before we begin creating your very first rust program, use the `cargo new hello_423 --vcs none` command. This will create a new binary project for you!

!!! info "Explaining what `cargo new hello_423 --vcs none` does"
    `cargo`: Cargo is a Rust package manager, similarly to Maven in Java (you may recall this if you took COMP301!)
    `new`: Keyword for creating a new project
    `--vcs none`: Necessary flag to prevent cargo from also creating a new `git` repo by default.  


### Writing and Running your very first Rust program!

1. Navigate to the `main.rs` file within `hello_423/src/`, here, you should see the following code snippet: 

```rust 
fn main() {
    println!("Hello, world!");
}
```

As you can see, this syntax is very similar to languages such as C and Java!

2. Change the code `println!("Hello, world!");` to `println!("Hello COMP423!");`.

3. Now, lets run your code! First, we must compile your program by first running `cargo build` after entering the `hello_423` directory.

!!! question "What does `cargo build` do?"
    The `cargo build` will compile your `.rs` file into a file that is ready to be run on the working machine. This is very similar to the `gcc -c app.c` command that will transform a `.c` file into a `.o` file.

4. Now, you should see a file named `Cargo.lock`, this file  contains information regarding your program's dependencies and allows your program to actually run. We are now ready to run the program! Run the code `cargo run`, and you should see the following output:

```Hello COMP423!```

!!! info "`cargo build` vs `cargo run`"
    The command `cargo build` is used to compile `.rs` code into a format where it can be turned into a program. On the other hand, the `cargo run` is typically used to execute the file that has just been compiled. However, if a compiled file does not exist, then the `cargo run` command will first compile the `.rs` file, and then run it.

Congratulations, you have written and ran your very first Rust program using the Cargo package manager!