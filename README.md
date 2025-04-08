# Research Computing Coursework: Sudoku Solver


[![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Cython](https://img.shields.io/badge/Cython-0033CC?style=flat-square&logo=python&logoColor=pink)](https://cython.org/)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?style=flat-square&logo=pre-commit&logoColor=white)](https://pre-commit.com/)
[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?&logo=docker&logoColor=white)](https://www.docker.com/)
[![configparser](https://img.shields.io/badge/configparser-Config-blue.svg)](https://docs.python.org/3/library/configparser.html)
[![Doxygen](https://img.shields.io/badge/Doxygen-documentation-purple.svg)](https://www.doxygen.nl/index.html)



## Contents
- [Motivation and Description](#motivation-and-description)
  - [Motivation](#motivation)
  - [Description](#description)
  - [Backtracking in Action](#backtracking-in-action)
- [Installation and Setup](#installation-and-setup)
  - [Cloning the Repository](#cloning-the-repository)
  - [Setting Up the Environment](#setting-up-the-environment)
    - [Option 1: Using Conda](#option-1:-using-conda)
    - [Option 2: Using Docker](#option-2:-using-docker)
- [Usage](#usage)
- [Features](#features)
- [Frameworks](#frameworks)
- [Build Status and Version Info](#build-status-and-version-info)
- [Credits](#credits)

## Motivation and Description
### Motivation

Sudoku, a well-known logic-based puzzle, poses a unique challenge: it's straightforward enough for humans to approach, yet complex enough to benefit from algorithmic solutions. This project aims to bridge the gap between human ingenuity and computational power, providing a tool that can assist puzzle enthusiasts and researchers alike in understanding and solving Sudoku puzzles efficiently.

The core of this motivation is the belief that every puzzle has a solution; it's just a matter of finding the right path. By leveraging modern programming techniques and optimization strategies, such as Cython for performance enhancement, we can create a robust solver that can tackle any puzzle from simple ones to harder.

### Description
This project is a sophisticated Sudoku solver implemented in Python, with performance optimizations using Cython. It's designed to tackle any Sudoku puzzle, from the simplest to the most complex, by employing a backtracking algorithm enhanced with a Minimum Remaining Values (MRV) heuristic. The solver not only guarantees a solution, if one exists, but also does so with remarkable speed and efficiency.

The solver's architecture is modular, allowing for clear separation between the puzzle input mechanism, the solving algorithm, and the output presentation. It can read puzzles from a file, solve them using either the Pythonic or Cythonic implementation, and output the solution in a human-readable format or save it to a file. Additionally, the solver is containerized using Docker, ensuring that the setup and execution process is seamless across different platforms and environments.

The project also features extensive documentation, tests for reliability, and continuous integration workflows, making it a robust tool for anyone interested in Sudoku, from casual players to algorithmic researchers. It embodies the spirit of open-source software, inviting contributions and improvements from the community.


### Backtracking in Action

![Sudoku Solver Animation](https://upload.wikimedia.org/wikipedia/commons/8/8c/Sudoku_solved_by_bactracking.gif)

## Installation and Setup

Before you begin the installation process, ensure you have the following prerequisites installed on your system:
- Install conda
- Python (3.11)
- Docker
- Git (for cloning the repository)

### Cloning the Repository

Clone the project repository from GitLab. Please ensure you have all permissions to access repository.
```bash
git clone https://gitlab.developers.cam.ac.uk/phy/data-intensive-science-mphil/c1_assessment/bs763.git
cd bs763
```
After successfully cloning the repo, there is two ways to set up the project.

### Setting Up the Environment

#### Option 1: Using Conda

You can set up the project using the `environment.yml` file, which contains all the necessary dependencies. Run the following command to create a Conda environment:

```bash
conda env create -f environment.yml --name bs763
```

This will create a new Conda environment specifically for this project. Once the environment is created, activate it using:
```bash
conda activate bs763
```
Note: Afterwards, make sure you install pre-commit inside the new conda environment

- Disclaimer: please double-check the environment name when created from environment.yml

Afterwards, make sure that cython is setup successfully by running the following commands:
```bash
cd cython_modules
python setup.py build_ext --inplace
```
or
```bash
python cython_modules/setup.py build_ext --inplace
```
#### Option 2: Using Docker

If you prefer to use Docker for setting up the environment, follow these steps. This method ensures that the project runs in a consistent environment, regardless of the host system's configuration.

1. **Build the Docker Image**

   First, you need to build a Docker image for the project. This image will contain the Miniconda environment and all necessary dependencies, as specified in your `Dockerfile`. Run the following command in the terminal:

   ```bash
   docker build -t bs763-sudoku-solver .
   ```
This command builds a Docker image named bs763-sudoku-solver using the Dockerfile in the *current directory*, meaning being inside the cloned directory \bs763
2. **Run the Docker Container**

After building the image, you can start a Docker container using this image. Run the following command:

```bash
docker run -it bs763-sudoku-solver
```
This command starts an interactive terminal session inside the container. Inside this container, the Conda environment named bs763 is already set up and activated. You can now run the Sudoku solver and other project-related commands within this container.

- Using the Project
With the container running, you're now in the environment where your project is set up with all dependencies. You can navigate through the project directory and use the project as intended. Every time you want to work on the project, you just need to start the Docker container with the `docker run` command.

- Finally, make sure that Cython is installed and if you can, reassure yourself that the .pyd file is inside in the cython_modules directory in the project (Dockerfile has been setup to run the necessary commands to set this up for you)
## Usage
The usage of the project is extremely straightforward, and has been constructed in such way to accomodate users with minimal programming experience. The user needs a sudoku.txt file as an input. The project is equipped with a configuration file, called parameters.ini, which can be easily editted:
```bash
[input]
input_one = experimentation_testing_cases/input_test.txt

[settings]
use_cython = True
print_solution = False
output_path = output/
```
As the project has both cythonic and pythonic features, you can define which way you would like to run the project by changing the `use_cython` cell. Also I have added a feature to either print the solution only, or if you would like the solution in the required format to be outputted to the folder `output`, with the following unique format: `f'{base_filename}_cython_{use_cython}_solution.txt'`.  Of course, you can change the input, just make sure it is the correct path. In addition, in the `solve_sudoku.py` main file, make sure to edit the cell: `sudoku_input_path = configuration['input']['input_one']` to reflect the required input as that in the `parameters.ini` file!.

- Afterwards, make sure you are in the base of the directory /bs763. Then, from the terminal, run:
```bash
python src/solve_sudoku.py parameters.ini
```
And depending on your settings in the parameters.ini file, you will receive the required output. The usage of parameters.ini allows the users to output multiple sudoku puzzle simultenously.

- Note: Please ensure that your Sudoku text file incomplete grid in the form of a text file with a 9x9 grid of numbers with zero representing unknown values and `|`,`+`,`-` separating cells and , i.e.:
```
$ cat input.txt
000|007|000
000|009|504
000|050|169
---+---+---
080|000|305
075|000|290
406|000|080
---+---+---
762|080|000
103|900|000
000|600|000
```
- The program is also equipped to assist the user if the input is not valid!

- **Using the profiling.py file**
 - Please ensure you are inside the src folder when running this module
## Documentation
Documentation is created by utilising Doxygen. The project already has a DOxyfile utilitised for this project, so what needs to be done by the user is to just navigate to `docs/` in the project and run doxygen in the terminal, the following way (ensure you are in the root of the project: /bs763):
```bash
cd docs/
doxygen
```
Afterwards, you will have a few generated files, from which the html folder golds the index.html file, where the documentation is being hosted. The generated HTML documentation can be viewed by pointing a HTML browser to the index.html file in the html directory. For the best results a browser that supports cascading style sheets (CSS) should be used (I'm using Mozilla Firefox, Google Chrome, Safari, and sometimes IE8, IE9, and Opera to test the generated output).

**You will be met with the README.md file as mainpage in doxygen with explanations**
- Note: I have included (with a lot of pain) some cython documentation in doxygen, but sadly it is limited as doxygen finds it hard even if I do a workaround with the .pyx file. So please read the docstrings in the `cython_module.pyx` to see what the functions do and how they function.

- Disclaimer: Please bare in mind that Doxygen finds it very hard creating documentation for .pyx files, even if I write it with Python style documentation. The logic and implementation of the cythonic function findMRV and checkvalidPos and their counterparts findMRV_pythonic and checkvalidPos_pythonic is the same, so the options for reading the docstrings is either by directly accessing the .pyx file and reading the explanation from there or just reading the documentation for the pythonic equivalents that are generated by doxygen.

## Features

- **Advanced Algorithm Implementation**: Leverages a sophisticated backtracking algorithm to solve Sudoku puzzles efficiently.
- **Heuristic Analysis**: Employs Minimum Remaining Values (MRV) heuristic to optimize the solving process by selecting the most constrained cells first.
- **Interactive Puzzle Input**: Allows users to input Sudoku puzzles in a convenient format and receive immediate feedback on the solution.
- **Solution Visualization**: Features a custom function to visually display the Sudoku solution in the terminal for quick assessment.
- **Cython Optimization**: Utilizes Cython for enhanced performance, significantly speeding up the computation-heavy aspects of the Sudoku solving algorithm.

## Frameworks
The technical stack and tools utilized in this project are selected for high performance, user-friendly experience, and consistent development practices:

- **Languages**: Implemented in [Python](https://www.python.org/) for its wide adoption and ease of use, with performance-critical sections optimized using [Cython](https://cython.org/).
- **Testing Framework**: Automated tests are conducted using [pytest](https://docs.pytest.org/en/stable/), chosen for its powerful yet simple-to-use features.
- **Code Quality Assurance**: Utilizes the [pre-commit framework](https://pre-commit.com/) to manage and maintain pre-commit hooks that run validations, formatting checks, and linting to enforce quality and consistency. (Using this instead because GitLab has quite a complex CI implementation)
- **Containerization**: The application is containerized with [Docker](https://www.docker.com/), encapsulating the environment and dependencies for consistent operation across various computing environments.

## Use of Chat-GPT and Co-Pilot

**Co-Pilot was not used in this project**

**Chat-GPT was used in a few instances throughout the project development**
- In this project, Chat-GPT version 3.5 was used in several places to aid in understanding erros, understanding concepts and code.
- Chat-GPT was used in utilities.py file to aid in debugging the code. It was also used to aid in the software development process whenever I ran into a problem, for example I got a pre-commit package error which I could not find the solution in Google, hence sought help from Chat-GPT.
- In addition, Chat-GPT was used to help in fixing a Cython error where I could not understand why I have ran into a numpy error in my .pyx file.
- Chat-GPT was used to generate doxy-style docstrings. In numerous instances the generated output for the docstrings had flawed logic or understanding of why and how to use the given functions, which was all editted by me to re-phrase or re-word majorly.
- Chat-GPT was not explicitly used to generate code. The project's inspiration is from open-source sudoku solvers, where I have cited those given functions in the .py they populate. In addition inspiration for Cython arises from Lecture 13 in the module Research Computing.

***NOTE: Most of this project is done mostly by referring to the extensive lecture notes in the Research Computing module, where in some places I have re-used code, for example in my Dockerfile I used the implementation that was presented to me in the final supervision class with Dr James Fergusson***

## Build Status and Version Info
- **2.1.1**:
  - Added more file handling cases
  - Build Status: Stable
  - Final Version
- **2.1.0**:
  - Fixed code readbility

- **2.0.0**:
  - Report included.
  - Added a test to check initial grid state.

- **1.2.0**:
  - Updated the algorithm to implement Cython.

- **1.1.0**:
  - Fixed bugs related to how the project is being run with imports.

- **1.0.0**:
  - Fully implemented backtracking algorithm with the minimum remaining values heuristic.

## Credits
Many thanks to Dr James Fergusson for his support and advice regarding the algorithm behind my sudoku solver, and mostly his patience in answering all of the questions about all aspects of the project in his free time. Without his help and expertise, the implementation of this sophisticated project would not be possible. I would like to also credit the amazing MPhil course for teaching me exceptionally amazing tools and techniques!
