# Setting up a dev container for Rust.

* Primary author: [Luke Allen](https://github.com/LukeAllen13)
* Reviewer: [Nicholas Cope](https://github.com/nicholas-cope)

Welcome to this tutorial on setting up a Rust project from scratch! By the end of this guide, you'll have a fully functional Rust development environment using **VS Code, Docker**, and **Git**, without installing Rust directly on your local machine. 

---

## *Prerequisites*
Before we begin, ensure you have:

- Visual Studio Code (VS Code): Download and install it from <a href="https://code.visualstudio.com/" target="_blank" rel="noopener noreferrer">here.</a>
- Docker installed: Required to run the dev container. <a href="https://www.docker.com/products/docker-desktop" target="_blank" rel="noopener noreferrer">Get Docker Here.</a>
- Git installed: <a href="https://git-scm.com/book/en/v2/Getting-Started-Installing-Git" target="_blank" rel="noopener noreferrer">Install Git</a> if you don't already have it.

---

## **Part 1: Setting up your Github Repository**

#### Step 1: Create a Local Directory and Initialize Git

(A) Open your terminal or command prompt.

(B) Create a new directory for your project or change into your desired directory. 

```
    mkdir rust-project
    cd rust-project
```

(C) Initialize a new Git repository:

```
    git init
```

(D) Create a README file:

```
    echo "# [your_name]'s Rust Project" > README.md
```

(E) Stage your changes:

```
git add .
```

(F) Make your first commit:

```
git commit -m "Added README.md file."
```

#### Step 2: Create a Remote Repository on GitHub

1. Go to <a href="https://github.com/" target="_blank" rel="noopener noreferrer">GitHub</a>, log in, and create a new repository named rust-project.

2. Follow the instructions GitHub provides to push your local repository to GitHub, similar to:
```
    git remote add origin https://github.com/[YOUR_USERNAME]/rust-project.git
    git push -u origin main
```

---

## **Part 2: Set up the Dev Container**

#### Step 1: Install the **Dev Containers** extension for VS Code

(A) Launch VS Code and open the Extensions view by pressing Ctrl + Shift + X or clicking the Extensions icon in the Activity Bar. 

(B) Search for and install the Dev Containers extension by Microsoft.

#### Step 2: Inside your project folder, create a ```.devcontainer``` directory with the following file inside of this "hidden" configuration directory:

```
.devcontainer/devcontainer.json
```

#### Step 3: Copy and Paste the following code and enter it into your ```devcontainer.json``` file.

```
{
  "name": "Rust Tutorial",
  "image": "mcr.microsoft.com/devcontainers/rust:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": [
        "rust-lang.rust-analyzer", 
        "matklad.rust-analyzer",
        "serayuzgur.crates",
        "vadimcn.vscode-lldb"
      ]
    }
  },
  "postCreateCommand": "cargo install --locked cargo-edit cargo-watch"
}
```

# Breakdown of `devcontainer.json`

- **`"name": "Rust Tutorial"`**  
    - Specifies the name of the development container environment.

- **`"image": "mcr.microsoft.com/devcontainers/rust:latest"`**  
    - Defines the base Docker image to be used, providing a preconfigured Rust environment.

- **`"customizations"`**  
    - Allows customization of the development environment, specifically for VS Code.

  - **`"vscode": { "settings": {} }`**  
    - Placeholder for custom VS Code settings (currently empty). 

  - **`"extensions"`**  
    - List of recommended VS Code extensions for Rust development:  
        - **`"rust-lang.rust-analyzer"`** – Official Rust language support with smart code analysis.  
        - **`"matklad.rust-analyzer"`** – Alternative Rust analyzer for enhanced autocompletion and navigation.  
        - **`"serayuzgur.crates"`** – Manages dependencies in `Cargo.toml` with suggestions and updates.  
        - **`"vadimcn.vscode-lldb"`** – Provides debugging support using LLDB for Rust applications.  

- **`"postCreateCommand": "cargo install --locked cargo-edit cargo-watch"`**  
    - Runs after the container is created to install additional Rust tools:  
        - **`cargo-edit`** – Adds commands to manage dependencies (`cargo add`, `cargo rm`, etc.).  
        - **`cargo-watch`** – Automatically rebuilds the project when changes are detected.  

#### Step 4: Reopen the Project in a VSCode Dev Container

(A) Reopen the project in the container by pressing ```Ctrl+Shift+P``` (For macOS: ```Cmd+Shift+P```), typing "Dev Containers: Reopen in Container," and selecting the option. 

(B) This may take a few minutes while the image is downloaded and the requirements are installed.

---

## **Part 3: Working with Rust**

#### Step 1: Check Rust Version

After the container setup completes, open a new terminal in VS Code and run:
```
rustc --version
```

You should see something like:
```
rustc 1.64.0 (a93df2f18 2024-03-23)
```

This confirms that a recent version of Rust is available in your dev container, meeting the requirement for an up-to-date version. 

#### Step 2: Create a New Rust Project

Now, let's create a new Rust binary project with the following command:

```
cargo new rust-project -vcs none
```

- The *-vcs none* flag prevents a cargo from initializing a Git repository automatically, as you'll manage the Git repository separately. 

#### Step 3: Write a Basic Rust Program

Navigate into your new project directory:

```
cd rust-project
```

Open the ```src/main.rs``` file and replace the contents with the following:

```
fn main(){
    println!("Hello COMP423");
}
```

#### Step 4: Build the Project

Now, build the project with:

```
cargo build
```

- This will compile the project, but won't run it yet. You'll find the compiled files in the target directory. This is like how in C, you might have to run a gcc [file_name] before running. 

#### Step 5: Run the Project

To run the project, use:

```
cargo run
```

- This command compiles and runs the project in one step. It's equivalent to running *cargo build* followed by executing the built file. 

You should see the output:

```
Hello COMP423
```



**Differences Between cargo build and cargo run:**

- ```cargo build```: This command compiles your project but doesn't run it.

- ```cargo run```: This command compiles (if needed) and then runs your project in one step.

---

## Conclusion

Congratulations! You've successfully set up a Rust development environment using a Dockerized dev container, installed the necessary extensions in VS Code, and learned how to create and manage a Rust project with ```cargo build``` and ```cargo run```. This approach ensures a consistent environment, avoiding the "it doesn't work on my machine" problem. It also keeps your local setup clean and organized, allowing you to just work on your Rust projects.

**Extra Note:** What do containers help with? Well, they prevent the above mentioned "it doesn't work on my machine" problem by ensuring everyone is working with the same software inside of the cloned project. In other words, containers are fully reproducible development environments that run inside of Docker containers, ultimately providing everything needed to work on a project consistently across different machines. 

# **Nice job getting through this tutorial!**