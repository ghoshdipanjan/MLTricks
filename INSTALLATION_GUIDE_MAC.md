# macOS Installation Guide

This beginner-friendly guide prepares a Mac to run the IATD Machine Learning Algorithms notebooks in Visual Studio Code.

The final setup uses a project-specific virtual environment stored permanently inside the repository. It does not depend on temporary folders.

---

# 1. Install Visual Studio Code

1. Visit [https://code.visualstudio.com/](https://code.visualstudio.com/).
2. Select **Download for Mac**. The universal build supports both Apple silicon and Intel Macs; choose the appropriate build if you prefer.
3. Open the downloaded `.zip` file.
4. Drag **Visual Studio Code.app** into the **Applications** folder.
5. Open Visual Studio Code from **Applications**. If macOS asks you to confirm opening an app downloaded from the internet, confirm that you want to open it.

---

# 2. Install Python

The course environment is designed for Python 3.12.

1. Visit [https://www.python.org/downloads/macos/](https://www.python.org/downloads/macos/).
2. Download the stable macOS installer for Python 3.12. The universal2 installer supports both Apple silicon and Intel Macs.
3. Open the downloaded `.pkg` installer and follow its instructions.
4. Do not use an experimental or alpha Python release for this course.

## Check Python

Open Terminal (or the VS Code terminal) and run:

```zsh
python3.12 --version
```

The result should begin with:

```text
Python 3.12
```

macOS does not use the Windows `py` launcher. Use `python3.12` in the commands in this guide.

If the command is not found after installing Python, try its standard python.org installation path:

```zsh
/Library/Frameworks/Python.framework/Versions/3.12/bin/python3.12 --version
```

Use that full path in place of `python3.12` in the virtual-environment creation command in section 7 if needed.

---

# 3. Install the VS Code extensions

In Visual Studio Code:

1. Select the **Extensions** icon on the left.
2. Search for **Python**.
3. Install the extension published by Microsoft.
4. Search for **Jupyter**.
5. Install the extension published by Microsoft.
6. Reload VS Code if prompted.

---

# 4. Store the repository permanently

Do not run notebooks directly from:

- An email attachment.
- A temporary browser preview.
- A ZIP archive.
- The macOS Downloads folder before extracting the repository to its permanent location.
- A temporary folder used by a browser or another application.

Extract or copy the repository to a permanent location, for example:

```text
/Users/YourName/source/IATD-Machine-Learning-Algorithms
```

The folder containing the notebooks should include:

```text
IATD-Machine-Learning-Algorithms/
├── 1_a_NumpyRefresher.ipynb
├── 1_b_PandasRefresher.ipynb
├── 1_c_MatplotlibRefresher.ipynb
├── requirements.txt
├── data/
├── provision/
└── .vscode/
```

The `data` folder contains the CSV files required by the notebooks.

---

# 5. Open the correct folder in VS Code

1. Open Visual Studio Code.
2. Select **File -> Open Folder**.
3. Select the innermost `IATD-Machine-Learning-Algorithms` folder: the folder that directly contains `requirements.txt` and the notebooks.
4. Select **Open**.
5. If VS Code asks whether you trust the folder, select **Yes, I trust the authors**, provided the repository came from a trusted course source.

Opening the complete folder is important because the notebooks use relative paths such as:

```python
pd.read_csv('data/matildas.csv')
```

---

# 6. Open the VS Code terminal

In VS Code:

1. Select **Terminal -> New Terminal**.
2. Check the terminal prompt.

It should show the repository folder, for example:

```text
YourName@MacBook-Pro IATD-Machine-Learning-Algorithms %
```

If the prompt shows a different folder, close the terminal and confirm that the correct repository folder is open in VS Code.

---

# 7. Create a permanent virtual environment

Run this command in the VS Code terminal:

```zsh
python3.12 -m venv .venv
```

If you needed the full python.org path in section 2, run:

```zsh
/Library/Frameworks/Python.framework/Versions/3.12/bin/python3.12 -m venv .venv
```

This creates:

```text
IATD-Machine-Learning-Algorithms/.venv
```

The environment is permanent and remains available whenever the repository is opened.

## Why use `.venv`?

Each Python project may require different package versions. The `.venv` gives this course its own:

- Python interpreter.
- NumPy installation.
- Pandas installation.
- Matplotlib installation.
- scikit-learn installation.
- Jupyter kernel.

Do not copy `.venv` to another computer. Each student should create it locally.

---

# 8. Install the pinned course packages

Run:

```zsh
./.venv/bin/python -m pip install --upgrade pip
./.venv/bin/python -m pip install -r requirements.txt
```

The second command installs the exact package versions against which the course notebooks were tested.

The installation can take several minutes because scientific packages such as NumPy, SciPy and scikit-learn are large.

Using the explicit `.venv` Python path ensures that packages are installed into the project environment rather than into an unrelated Python installation. These commands work in the default macOS zsh shell and do not require environment activation.

---

# 9. Register an easy-to-recognise Jupyter kernel

Run:

```zsh
./.venv/bin/python -m ipykernel install --user --name iatd-ml --display-name "IATD ML (Python 3.12)"
```

This creates a persistent kernel choice named:

```text
IATD ML (Python 3.12)
```

It can be selected whenever one of the course notebooks is opened.

---

# 10. Select the Python interpreter

In VS Code:

1. Press **Cmd+Shift+P**.
2. Type `Python: Select Interpreter`.
3. Select the command.
4. Choose the interpreter labelled `.venv`.

Its path should end with:

```text
IATD-Machine-Learning-Algorithms/.venv/bin/python
```

If it does not appear:

1. Select **Enter interpreter path**.
2. Select **Find**.
3. Browse to `.venv/bin/python` inside the repository.
4. Select it.

The repository's `.vscode/settings.json` file also tells VS Code to prefer this environment.

---

# 11. Select the notebook kernel

1. Open `1_a_NumpyRefresher.ipynb`.
2. Select the kernel name in the notebook's top-right corner.
3. Select **Select Another Kernel**, if required.
4. Select **Python Environments** or **Jupyter Kernel**.
5. Choose:

```text
IATD ML (Python 3.12)
```

or the repository's:

```text
.venv (Python 3.12)
```

Do not choose an interpreter from a temporary folder or an experimental Python installation.

---

# 12. Test the environment

In a notebook code cell, run:

```python
import sys
import numpy as np
import pandas as pd
import matplotlib
import sklearn
import ipykernel

print("Python:", sys.version)
print("Interpreter:", sys.executable)
print("NumPy:", np.__version__)
print("Pandas:", pd.__version__)
print("Matplotlib:", matplotlib.__version__)
print("scikit-learn:", sklearn.__version__)
print("IPython kernel:", ipykernel.__version__)
```

The interpreter path should contain:

```text
IATD-Machine-Learning-Algorithms/.venv/bin/python
```

The core course versions should include:

```text
NumPy: 1.26.4
Pandas: 2.2.2
Matplotlib: 3.9.2
scikit-learn: 1.5.1
```

---

# 13. Run the official smoke test

The repository includes a verification program that:

- Checks the important package versions.
- Executes every lab notebook from top to bottom.
- Reports any failing notebook.

From the repository root, run:

```zsh
./.venv/bin/python provision/smoke_test.py
```

Some later notebooks may take several minutes.

A successful result ends with:

```text
SMOKE TEST PASSED - environment matches and all labs run clean.
```

---

# 14. Run notebooks in VS Code

## Run one cell at a time

Select the triangular **Run Cell** button beside a code cell.

This approach is recommended while learning because students can:

- Observe each result.
- Connect code with output.
- Stop when something is unclear.
- Change values and experiment.

Run cells from top to bottom because later cells often depend on variables created earlier.

## Run the complete notebook

From the notebook toolbar, select:

```text
Restart Kernel and Run All
```

This clears previous variables and proves that the notebook works from a clean state.

---

# 15. Recommended learning order

Begin with:

1. `1_a_NumpyRefresher.ipynb`
2. `1_b_PandasRefresher.ipynb`
3. `1_c_MatplotlibRefresher.ipynb`

Then continue through the numbered notebooks in order.

The first three establish the foundations used by the later machine-learning labs.

---

# 16. Everyday workflow

The setup only needs to be completed once.

Each day:

1. Open Visual Studio Code.
2. Select **File -> Open Recent**.
3. Open the innermost `IATD-Machine-Learning-Algorithms` folder.
4. Open the required notebook.
5. Check the kernel in the top-right corner.
6. Select `IATD ML (Python 3.12)` if another kernel is shown.
7. Run cells individually or select **Restart Kernel and Run All**.

Do not reinstall packages every day.

---

# Troubleshooting

## Running cells requires `ipykernel`

The wrong Python environment is probably selected.

Select the notebook kernel:

```text
IATD ML (Python 3.12)
```

If necessary, reinstall `ipykernel` into the project environment:

```zsh
./.venv/bin/python -m pip install ipykernel==6.29.5
```

## `No module named numpy`, `pandas` or `matplotlib`

The package may have been installed into another Python environment.

Reinstall all pinned dependencies into `.venv`:

```zsh
./.venv/bin/python -m pip install -r requirements.txt
```

Then select the `.venv` kernel again.

## `.venv` does not appear

1. Press **Cmd+Shift+P**.
2. Run **Developer: Reload Window**.
3. Run **Python: Select Interpreter**.
4. Select `.venv`.
5. Open the notebook and select its kernel again.

## `python3.12` is not found

Confirm that Python 3.12 was installed from python.org. Try:

```zsh
/Library/Frameworks/Python.framework/Versions/3.12/bin/python3.12 --version
```

If this prints Python 3.12, use that full path to create `.venv` as shown in section 7. Do not substitute Apple's system `python3` unless it reports Python 3.12.

## Permission or command errors while installing packages

Do not use `sudo` or install course packages globally. Confirm that `.venv` exists in the repository and run pip through its interpreter:

```zsh
./.venv/bin/python -m pip install -r requirements.txt
```

If `.venv/bin/python` does not exist, repeat the virtual-environment creation step from the repository root.

## A CSV file cannot be found

Check that:

- VS Code opened the innermost repository folder.
- The `data` folder exists.
- The expected CSV exists inside `data`.
- The repository was fully extracted from its ZIP archive.
- The notebook is not being run directly from an attachment.

For the Pandas refresher, the expected file is:

```text
data/matildas.csv
```

## Cells behave strangely or variables contain old values

Jupyter permits cells to be executed in any order, so old values can remain in memory.

Select:

```text
Restart Kernel and Run All
```

This clears the kernel and runs the notebook from top to bottom.

## Matplotlib creates image files

The Matplotlib refresher writes files such as:

```text
plot1.png
figure.png
```

These appear in the repository folder after the relevant cells execute.

---

# Setup checklist

Before beginning the course, confirm:

- [ ] Visual Studio Code is installed.
- [ ] The Microsoft Python extension is installed.
- [ ] The Microsoft Jupyter extension is installed.
- [ ] Stable Python 3.12 is installed.
- [ ] The repository is in a permanent folder.
- [ ] The innermost repository folder is open in VS Code.
- [ ] `.venv` exists inside the repository.
- [ ] `requirements.txt` has been installed into `.venv`.
- [ ] `IATD ML (Python 3.12)` is selected as the notebook kernel.
- [ ] `data/matildas.csv` and the other datasets are present.
- [ ] The official smoke test passes.
