
# Sorting Algorithms, Engineering Lab

[![build](../../actions/workflows/build.yml/badge.svg)](../../actions/)
![Platforms: Linux, MacOS, Windows](https://img.shields.io/badge/Platform-Linux%20%7C%20MacOS%20%7C%20Windows-blue.svg)
[![Language: Python](https://img.shields.io/badge/Language-Python-blue.svg)](https://www.python.org/)
[![Code Style: Black](https://img.shields.io/badge/Code%20Style-Black-blue.svg)](https://github.com/psf/black)
[![Commits: Conventional](https://img.shields.io/badge/Commits-Conventional-blue.svg)](https://www.conventionalcommits.org/en/v1.0.0/)
[![Discord](https://img.shields.io/discord/872320492936257537?logo=discord)](https://discord.gg/kjah8MFYbR)

## Introduction

Different sorting algorithms have different time complexities. The complexity
can be worked out theoretically by examining the code constructs within
the algorithms. However, it is also possible to empirically work out the
complexity by running doubling experiments.

Doubling experiments repeatedly double the input size to an algorithm. The
doubling ratio of the output can then be computed, and used to determine the
apparent time complexity of the algorithm.

The sorting algorithms that will be tested are:

- bubble sort
- insertion sort
- merge sort
- quick sort
- tim sort

## Learning Objectives

The learning objectives of this assignment are to:

1. Run a doubling experiment to compare sorting algorithms empirically
2. Use big-O notation to characterize sorting algorithms
3. Use Git and GitHub to manage source code file changes
4. Use VS Code Markdown Preview to view mathematical expressions
5. Write clearly about the programming concepts in this assignment.

## Quick Links

- Due date: Check Discord or the
  [Assignment Schedule](https://allegheny-college-cmpsc-101-spring-2025.github.io/site/materials.html)
- Policy on
  [Tokens](https://allegheny-college-cmpsc-101-spring-2025.github.io/site#tokens)
- [#data-structures Discord channel](https://discord.com/channels/877320365825749002/1326565523042992159)
- [Starter repo](https://github.com/allegheny-college-cmpsc-101-spring-2025/sorting-algorithms-starter)

## Project Goals ([Project Overview](#project-overview) Below)

This engineering lab invites you to implement and use a program called
`listsorting` that performs a doubling experiment to evaluate the performance of
several different sorting algorithms. First, you will follow the [Sorting
Algorithms in Python](https://realpython.com/sorting-algorithms-python/)
tutorial from [Real Python](https://realpython.com/) and add certain sorting
algorithms, like bubble sort and quick sort, to your project. After you have
implemented all of the required sorting algorithms, you will use the provided
benchmarking framework to conduct a doubling experiment. This doubling
experiment will invoke a specific sorting algorithm while repeatedly doubling
the size of the input to the sorting algorithm for a specific number of doubling
rounds. Since the doubling experiment enables you to calculate a doubling ratio,
it enables you to experimentally predict the likely worst-case time complexity
of each sorting algorithms. In addition to implementing the sorting algorithms
and extending the benchmarking framework, you will use a comprehensive
command-line interface, implemented with [Typer](https://typer.tiangolo.com/),
that allows you to easily control the execution of a doubling experiment.
Finally, you will use your empirical results from using the `listsorting`
program to better understand the performance trade-offs associated with sorting
algorithms implemented in Python.

### Expected Output

This project invites you to implement a Python program, called `listsorting`
that performs a doubling experiment to evaluate the performance of several
different sorting algorithms. After you finish a correct implementation of all
the program's features, running it with the command `poetry run listsorting
--starting-size 100 --number-doubles 5 --approach insertion`, causes it to
produce output like the following. With that said, please remember that when you
run the `listsorting` program your computer it will likely produce different
performance results! Importantly, this output shows that the `listsorting`
program ran the insertion sort algorithm, denoted `insertion`, for a total of
`5` rounds in a doubling experiment that created input sizes that ranged from
`100` to `1600`. When `listsorting` runs the experiment, it uses the
[timeit](https://docs.python.org/3/library/timeit.html) package to measure the
`min`, `max`, and `avg` execution time of the algorithm.

```text
✨ Conducting an experiment to measure the performance of list sorting!

   The chosen sorting algorithm: insertion
   Starting size of the data container: 100
   Number of doubles to execute: 5

✨ Here are the results from running the experiment!

  Input Size    Min time (s)    Max time (s)    Avg time (s)
------------  --------------  --------------  --------------
         100         0.00198         0.00228         0.0021
         200         0.00791         0.00831         0.00804
         400         0.03091         0.03179         0.03129
         800         0.1397          0.14232         0.141
        1600         0.56098         0.58918         0.57665
```

These experimental results suggest that insertion sort has a doubling ratio of
$\frac{0.57665}{0.141} \approx 4.0897$. If you look at the last row of the data
table you will see that, for the input sizes of `1600` and `800`, the average
execution time for insertion sort was $0.57665$ and $0.141$ seconds,
respectively. Dividing the execution time for the larger input size by the
execution time of the smaller input size yields the doubling ratio of
approximately $4.0897$, suggestion that insertion sort is a $O(n^2)$ algorithm
because a doubling of the input size caused a quadrupling of the execution time.
Moreover, don't forget that you can display `listsorting`'s help menu and learn
more about its features by typing `poetry run listsorting --help` to show the
following output. Finally, remember that the `listsorting` program should also
run experiments for the other sorting algorithms, such as bubble sort and quick
sort! You can also run `listsorting` with larger input sizes or more rounds of
input doubling --- but be aware of the fact that your experiments could take a
long time to finish for certain algorithms!

```text
╭─ Options ─────────────────────────────────────────────────────────────╮
│ --starting-size             INTEGER              [default: 1000000]   │
│ --maximum-value             INTEGER              [default: 10000]     │
│ --number-doubles            INTEGER              [default: 10]        │
│ --approach                  [bubble|insertion|m  [default: bubble]    │
│                             erge|quick|tim]                           │
│ --install-completion        [bash|zsh|fish|powe  Install completion   │
│                             rshell|pwsh]         for the specified    │
│                                                  shell.               │
│                                                  [default: None]      │
│ --show-completion           [bash|zsh|fish|powe  Show completion for  │
│                             rshell|pwsh]         the specified shell, │
│                                                  to copy it or        │
│                                                  customize the        │
│                                                  installation.        │
│                                                  [default: None]      │
│ --help                                           Show this message    │
│                                                  and exit.            │
╰───────────────────────────────────────────────────────────────────────╯
```

Please note that the provided source code does not contain all of the
functionality to produce the output displayed in this section. As the next
section explains, you should add the features needed to ensure that
`listsorting` produces the expected output! Drawing from the source code
provided in the aforementioned [Sorting Algorithms in
Python](https://realpython.com/sorting-algorithms-python/) tutorial from [Real
Python](https://realpython.com/), this project invites you to add all of the
sorting algorithms, use the `listsorting` program to conduct a doubling
experiment for each of the sorting algorithms and, finally, leverage the data
tables of empirical results to calculate a doubling ratio and predict the likely
worst-case time complexity of each sorting algorithm.

Don't forget that if you want to run the `listsorting` program you must use
your terminal window to first go into the GitHub repository containing this
project and then go into the `listsorting/` directory that contains the
project's source code. Finally, remember that before running the program you
must run `poetry install` to add its dependencies, such as Pytest for
automated testing and Rich for colorful output!

### Adding Functionality

If you study the file `listsorting/listsorting/sorting.py` you will see that it
has many `TODO` markers that designate the sorting algorithms that you must
implement so as to ensure that `listsorting` will produce correct output. For
instance, you will need to provide an implementation of each sorting algorithm,
like bubble sort, that has a signature like `def bubble_sort(array: List[int])
-> List[int]`. You will also need to resolve all of the `TODO` markers in
`listsorting/listsorting/main.py` that involve calling the functions in
`listsorting/listsorting/experiment.py` to run each of the steps in a doubling
experiment. Specifically, you must ensure that the `listsorting` function in the
`main` module calls the following `run_sorting_algorithm_experiment_campaign`
function. Once you complete a task associated with a `TODO` marker, make sure
that you delete it and revise the prompt associated with the marker into a
meaningful comment.

```python
def run_sorting_algorithm_experiment_campaign(
    algorithm: str,
    starting_size: int,
    maximum_value: int,
    number_doubles: int,
) -> List[List[Union[int, Tuple[float, float, float]]]]:
    data_table = []
    while number_doubles > 0:
        random_list = generate_random_container(starting_size, maximum_value)
        performance_data = run_sorting_algorithm(algorithm, random_list)
        data_table_row = [
            starting_size,
            performance_data[0],
            performance_data[1],
            performance_data[2],
        ]
        data_table.append(data_table_row)
        number_doubles = number_doubles - 1
        starting_size = starting_size * 2
    return data_table
```

Notably, the `run_sorting_algorithm_experiment_campaign` function completes all
of the steps associated with running a specified sorting algorithm in a doubling
experiment. Upon completion, this function returns a `data_table` that contains
performance results for each round of the doubling experiment, as shown in the
previous section. After finishing your implementation of `listsorting`,
including the call to `run_sorting_algorithm_experiment_campaign` in `main`, you
should repeatedly run the program in different configurations to conduct an
experiment to evaluate the performance of each sorting algorithm that you
implemented. This process will result in a data table that summarizes the
results from a doubling experiment for each sorting algorithm. You can use the
data in the table to calculate the doubling ratio and then use it to predict the
likely worst-case time complexity of each sorting algorithm.

## Running Checks

### Helper Tasks

Helper tasks are run in the terminal with the poetry environment activated.
The format of the commands are always `poetry run task xyz`...where `xyz`
is the helper task name.

If you study the source code in the `pyproject.toml` file you will see that it
includes the following section that specifies different executable "helper
task" names like `ruff`, `fix`, `ruffdetails`, etc.

```toml
[tool.taskipy.tasks]
```

If you are in the `objectprocessor` directory that contains the
`pyproject.toml` file, the helper tasks
make it easy to run commands like `poetry run task ruff` to automatically run
the ruff linter designed to check the Python source code in your program
to confirm that your source code adheres to industry standards for formatting.
You can also use the command `poetry run task fix` to automatically reformat the
source code. `poetry run task ruffdetails` will print out detailed linting errors
that point to exactly what ruff views as a linting error. Make sure to examine
the `pyproject.toml` file for other convenient tasks that you can use to both
check and improve your project!

### Gatorgrade

The command `gatorgrade --config config/gatorgrade.yml` will check your work. If
your work meets the baseline requirements and adheres to the best practices that
proactive programmers adopt you will see that all the checks pass when you run
`gatorgrade`. Try to pass as many checks as you can. Missing some checks will only
impact a part of your grade in this Engineering Lab. Note, modifications to the
gatorgrade.yml file are not permitted without explicit instruction.

### Pytest

If your program has
all of the anticipated functionality, you can run the command `poetry run task
test` and see that the test suite produces output like the following.

```text
tests/test_sorting.py ...
```

Add comments to the test suite to explain how the test cases work. It is worth
noting that the name of the test suite is `test_sorting` because the
functions mentioned in the previous section exist in the `listsorting` module.

Don't forget that when you commit source code or technical writing to your
GitHub repository for this project, it will trigger the run of a GitHub
Actions workflow. If you are a student at Allegheny College, then running
this workflow consumes build minutes for the course's organization! As
such, you should only commit to your repository once you have made
substantive changes to your project and you are ready to confirm its
correctness. Before you commit to your GitHub repository, you can still run
checks on your own computer by using Poetry and GatorGrader. You can also
add and commit work locally before pushing it by using git commands in the
terminal: `git add .` and `git commit -m "Commit Message"`.

### Project Reflection

Once you have finished both of the previous technical tasks, you can use a text
editor to answer all of the questions in the `writing/reflection.md` file. For
instance, you should provide the output of the Python program in a fenced code
block, explain the meaning of the Python source code segments that you
implemented, and answer all of the other questions about your experiences in
completing this project. A specific goal of the reflection for this project is
to ensure that you can clearly write research questions and an experiment
methodology for assessing the performance of a sorting algorithm through a
doubling experiment. Once you have finished addressing the prompts in the
`writing/reflection.md` file that have `TODO` makers given as reminders, make
sure that you either delete the prompt or carefully integrate a revised version
of it into your writing.

### Project Assessment

Since this project is an engineering effort, it is aligned with the
**evaluating** and **creating** levels of [Bloom's
taxonomy](/proactive-learning/blooms-taxonomy/). You can learn more about how a
proactive programming expert will assess your work by examining the [assessment
strategy](/proactive-learning/assessment-strategy/). From the start to the end
of this project you may make an unlimited number of reattempts at submitting
source code and technical writing that meet all aspects of the project's
specification.

## Project Overview

After cloning this repository to your computer, please take the following
steps:

- Use the `cd` command to change into the directory for this repository.
- Specifically, you can change into the program directory by typing `cd listsorting`.
- Install the dependencies for the project by typing `poetry install`.
- Run the program with its different configurations by typing:
  - `poetry run listsorting --starting-size 1024 --number-doubles 5 --approach tim`
  - Note that this is not the only configuration you should try for your experiment
  - Note that the program will not work unless you add the required source code
  - Refer to the `writing/reflection.md` for details about designing your experiment
- Please note that the program will not work unless you add the required
  source code at the designated `TODO` markers.
- Confirm that the program is producing the expected output described
  [above](#expected-output)
- Run the automated grading checks by typing
  `gatorgrade --config config/gatorgrade.yml`.
- You may also review the output from running GatorGrader in GitHub Actions.
- Don't forget to provide all of the required responses to the technical writing
  prompts in the `writing/reflection.md` file.
- Please make sure that you completely delete the `TODO` markers and their
  labels from all of the provided source code.
- Please make sure that you also completely delete the `TODO` markers and their
  labels from every line of the `writing/reflection.md` file.
- Finally, submit your work to GitHub using git.
