# Setting up a dev container for Rust

* Primary author: [Kaw Bu](https://github.com/kawbu)

## Prerequisites

Before we dive in, make sure you have:

1. **A [GitHub](https://www.github.com) account** 
2. **[Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) already installed**
3. **[Visual Studio Code](https://code.visualstudio.com/)**
4. **[Docker preinstalled](https://www.docker.com/products/docker-desktop)**
5. **COMP211**

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
2. Install the **Dev Containers** extension for VS Code
3. Create a `.devcontainer` directory in the root of your project with the following file inside of this "hidden" configuration directory:

`.devcontainer/devcontainer.json`

The `devcontainer.json` file defines the configuration for your development environment. Here, we're specifying the following:

-`name`: A descriptive name for the container.  
-`image`: The docker image to use.  
-`customizations`: Adds useful configurations to VS Code.  
-`postCreateCommand`: A command to run after the container has been created.  

A dev container

### What is Rust?

Rust is a fast and efficient programming language published on May 15, 2015. It is widely used for the creation of low-level projects, such as Operating Systems. It is favored by many people for multiple reasons, such as:

- Efficient Stack/Heap Storage
- Many Safety Features
- A Strong Ecosystem


### Basic Rust Syntax

Here is a simple "Hello 423!" implementation for Rust:

```
fn main() {

  println!("Hello 423!");

}
```

As you can see, this is very similar to languages such as C and Java!
