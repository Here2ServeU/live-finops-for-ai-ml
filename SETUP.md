# Set up your lab: FinOps for AI-ML Systems

When you finish this page you will have the course lab on a Linux terminal, a month of pretend AI cloud bills generated, and a health check showing all OK. It takes about 10 to 15 minutes.

## What you need

- Any computer: Windows, Mac or Linux. A browser alone is enough if you use Codespaces.
- About 50 MB of free disk space.
- A free GitHub account (only for Option A, Codespaces).
- A Linux terminal: Codespaces, WSL Ubuntu on Windows, or a Multipass VM on a Mac.
- Python 3.9 or newer, and git.
- No pip install. The lab uses only Python's standard library.
- No GPU. The GPUs in the lab are simulated.
- No cloud account and no API keys. The bills are simulated, so you cannot run up a real bill by accident.

## Step 1 · Pick where to run it

### Option A: GitHub Codespaces (easiest, in your browser)

1. Sign in to GitHub and open this repo.
2. Click **Code > Codespaces > Create codespace on main**.
3. Wait for the terminal to open at the bottom. Python 3 and git are already installed.

### Option B: Windows (WSL / Ubuntu)

1. Open **PowerShell as Administrator** and run:
   ```powershell
   wsl --install -d Ubuntu-24.04
   ```
2. Restart your computer, then open **Ubuntu** from the Start menu and create a Linux username and password.
3. In the Ubuntu terminal, install the tools:
   ```bash
   sudo apt update
   sudo apt install -y git python3 unzip
   ```

### Option C: Mac (Multipass VM)

1. Install Homebrew first (see brew.sh), then Multipass:
   ```bash
   brew install --cask multipass
   ```
2. Create and open an Ubuntu VM:
   ```bash
   multipass launch 24.04 --name ailab
   multipass shell ailab
   ```
3. Inside the VM, install the tools:
   ```bash
   sudo apt update
   sudo apt install -y git python3 unzip
   ```

## Step 2 · Get the lab files

Download [Lab_Repo_finops-for-ai-ml.zip](downloads/Lab_Repo_finops-for-ai-ml.zip) from the `downloads/` folder of this repo.

- **Codespaces:** the file is already there, in `downloads/`.
- **WSL:** your Windows Downloads folder is at `/mnt/c/Users/<your-windows-name>/Downloads/`. Copy the file into your Linux home:
  ```bash
  cp /mnt/c/Users/<your-windows-name>/Downloads/Lab_Repo_finops-for-ai-ml.zip ~/
  ```
- **Multipass:** in a Mac terminal (not inside the VM), send the file into the VM:
  ```bash
  multipass transfer ~/Downloads/Lab_Repo_finops-for-ai-ml.zip ailab:
  ```

The zip has no top folder, so unzip it into a new folder and step into it:

```bash
cd ~
unzip Lab_Repo_finops-for-ai-ml.zip -d finops-for-ai-ml
cd finops-for-ai-ml
ls
```

In Codespaces, use the path `downloads/Lab_Repo_finops-for-ai-ml.zip` in the `unzip` command instead.

You should see `README.md`, `SCRIPTS.md`, `lab`, `module-1`, `module-2`, `module-3`, `setup` and `tests`.

## Step 3 · Install and check

There is nothing to install with pip. Make the lab data, then run the health check. Always run commands from the `finops-for-ai-ml` folder.

```bash
python3 lab/make_data.py
bash setup/doctor.sh
```

You should see:

```
wrote data/bill.csv (344 lines, $5,778 this month), usage.csv, gpu_util.csv, history.csv (90 days)
```

and then every doctor line marked `[ OK ]`: Linux, Python, Python 3.9 or newer, git, and `lab data ready`.

Optional: run the six built-in checks.

```bash
python3 -m unittest discover tests
```

You should see `Ran 6 tests` and `OK`.

## Step 4 · Quick test for each module

All prices in `lab/prices.json` are made-up lab prices, chosen to be easy to work with.

**Module 1 · See Every Dollar**

```bash
python3 module-1/top.py
python3 module-1/tag_audit.py; echo "exit $?"
```

You should see `This month: $5,778`, with `gpu.small $2,160 37.4%` at the top. The audit shows `Spend with no team tag: $1,620 of $5,778 = 28%`, then `RESULT: FAIL` and `exit 1`. To fix the tags and pass:

```bash
cp module-1/tags.example.json module-1/tags.json
python3 module-1/tag_audit.py
python3 module-1/showback.py
```

You should see `RESULT: PASS`, and research as the biggest spender at `$2,273`.

**Module 2 · Cut the Waste, Not the Model**

```bash
python3 module-2/idle.py
python3 module-2/llm_router.py
```

You should see notebook-gpu-03 marked `DELETE` and `Estimated saving: $1,897 per month`. In the router table, `route + cache` costs about $102 a month with 98.9% quality, which is a `PASS`.

**Module 3 · Budgets That Bite**

```bash
python3 module-3/anomaly.py
python3 module-3/cost_gate.py module-3/change-ok.json
python3 module-3/cost_gate.py module-3/change-bad.json; echo "exit $?"
```

You should see `ALERT day 74: research spent $791 (normal $22, 36x)`. The good change shows `+$144 per month` and `RESULT: PASS`. The bad change shows `+$11,520 per month`, a FAIL and `exit 1`.

## If something goes wrong

- **Doctor says "lab data missing".** Run `python3 lab/make_data.py` from the `finops-for-ai-ml` folder, then run the doctor again.
- **`No such file or directory` or `can't open file`.** You are in the wrong folder. Run `cd ~/finops-for-ai-ml` (in Codespaces, go to the folder you unzipped into), then try again.
- **Doctor says "not Linux".** You are in a Mac or Windows terminal. Use Codespaces, WSL Ubuntu or the Multipass VM.
- **`unzip: command not found` or `git missing`.** Run `sudo apt update && sudo apt install -y unzip git python3`.
- **The tag audit still says FAIL after the fix.** Check that `module-1/tags.json` exists. The copy command must be run from the `finops-for-ai-ml` folder.
- **Stuck for 15 minutes?** Switch to Option A, Codespaces. It works in any browser with nothing to install.

## Official guides

- GitHub Codespaces: https://docs.github.com/codespaces
- Install WSL on Windows: https://learn.microsoft.com/windows/wsl/install
- Install Multipass on a Mac: https://canonical.com/multipass/install
- Python downloads: https://www.python.org/downloads/
