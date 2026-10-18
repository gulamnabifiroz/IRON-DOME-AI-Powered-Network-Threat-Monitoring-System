# IRON DOME — Installation Guide

## 1. Prerequisites

Install the following before starting:

- Python 3.12
- Git
- Suricata IDS (on the system monitoring network traffic)
- A Google Gemini API key for AI analysis

Python: https://www.python.org/downloads/

Git: https://git-scm.com/downloads

Gemini API key: https://aistudio.google.com/apikey

## 2. Clone the Repository

Open Windows CMD and run:

```cmd
git clone https://github.com/gulamnabifiroz/IRON-DOME.git
cd IRON-DOME
```

Replace `YOUR_USERNAME` with your GitHub username and use your actual repository name.

If you have already downloaded the repository, open CMD inside the project folder.

## 3. Create a Virtual Environment

```cmd
py -3.12 -m venv .venv
```

Activate it:

```cmd
.venv\Scripts\activate
```

Upgrade pip:

```cmd
python -m pip install --upgrade pip
```

## 4. Install Python Libraries

Create a file named `requirements.txt` containing:

```text
PySide6
keyring
```

Install the dependencies:

```cmd
python -m pip install -r requirements.txt
```

Verify the installation:

```cmd
python -c "import PySide6; print('PySide6 installed')"
python -c "import keyring; print('Keyring installed')"
```

**Note:** `keyring` is optional if the application uses its environment-variable fallback. Modules such as `sqlite3`, `json`, and `urllib` are included with Python and do not need separate installation.

## 5. Configure Gemini API

Obtain your API key from:

https://aistudio.google.com/apikey

In Windows CMD, set the key for the current session:

```cmd
set GEMINI_API_KEY=YOUR_GEMINI_API_KEY
```

Replace the placeholder with your actual API key.

Alternatively, enter the key through the Gemini settings dialog in the application.

Do not upload your API key to GitHub.

## 6. Install Suricata

Suricata is installed separately from Python libraries.

On Debian or Raspberry Pi OS, open a terminal and run:

```bash
sudo apt update
sudo apt install -y suricata suricata-update jq
sudo suricata-update
sudo suricata -T -c /etc/suricata/suricata.yaml
sudo systemctl enable suricata
sudo systemctl restart suricata
```

Check its status:

```bash
sudo systemctl status suricata
```

A common Suricata event log path is:

```text
/var/log/suricata/eve.json
```

Ensure Suricata is monitoring the correct network interface and that IRON DOME can access the configured event source.

## 7. Run IRON DOME

From the activated virtual environment and project directory, run:

```cmd
python IRON_DOME.py.
```

If your Python file has a different name, replace the filename in the command.

## 8. Troubleshooting

**PySide6 not found:**

```cmd
python -m pip install PySide6
```

**Keyring not found:**

```cmd
python -m pip install keyring
```

**Gemini connection failure:**

- Verify your API key.
- Check your internet connection.
- Verify that the configured Gemini model is available to your API account.

**No Suricata events:**

- Check that Suricata is running.
- Verify the network interface and event-log path.
- Confirm that the monitored traffic reaches the Suricata sensor.

## Security Notice

Use IRON DOME only on networks and systems you are authorized to monitor. Keep API keys and sensitive incident logs private.
