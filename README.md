# Pattern Recognition

Coursework for the Pattern Recognition course.

## Environment setup

These steps are for Linux with Anaconda installed in `~/anaconda3`.

### 1. Make `conda` available in the shell (one-time)

```bash
~/anaconda3/bin/conda init bash
```

Then open a new terminal.

### 2. Create the `pr` environment

```bash
conda create --name pr
conda activate pr

conda install numpy matplotlib pandas seaborn scipy pip
pip install -U "scikit-learn<1.8"
pip install yellowbrick
conda install -c conda-forge notebook
```

Notes:
- `pip` is installed into the environment so the `pip install` commands
  install into `pr`, not into another Python.
- scikit-learn is pinned below 1.8. yellowbrick 1.5 detects classifiers via
  the `_estimator_type` attribute, which scikit-learn 1.8 removed. With a
  newer scikit-learn, visualizers such as `ConfusionMatrix` fail with
  *"This estimator is not a classifier"*.

### 3. Verify

Open `test_env.ipynb` and run all cells. It prints the interpreter and package
versions, then trains a classifier on the Iris dataset and plots a yellowbrick
confusion matrix. Expected: the interpreter path contains `envs/pr` and the
test accuracy is about 0.97.

To run it in the browser instead of VS Code:

```bash
conda activate pr
jupyter notebook
```

## VS Code

`.vscode/settings.json` points VS Code at the `pr` environment, so when this
folder is opened:
- Python files run with `pr`.
- New integrated terminals activate `pr` automatically.
- Notebooks default to the `pr` kernel. If one doesn't, click **Select Kernel**
  → **Python Environments** → **pr**.

The settings use absolute paths under `/home/manos/anaconda3`. On another
machine, edit those paths or pick the interpreter with
**Python: Select Interpreter** (`Ctrl+Shift+P`).

Required extensions: **Python** (`ms-python.python`) and **Jupyter**
(`ms-toolsai.jupyter`).
