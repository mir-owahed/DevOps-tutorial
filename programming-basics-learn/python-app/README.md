# how to install python on ubuntu
```
sudo apt install python3 python3-pip build-essential python3-dev 
python3 -V
pip3 -V

# NOTE: You may need to use 'sudo' to install the dependencies globally
pip3 install -r requirements.txt

python3 app.py
```

Create python virtual environment
```
apt install python3.12-venv
python3 -m venv venv
source venv/bin/activate
deactivate
```
## uv : An extremely fast Python package and project manager, written in Rust.
```
curl -LsSf https://astral.sh/uv/install.sh | sh
uv python install
mkdir hello-world
cd hello-world
uv init
```

Creating a virtual environment
```
uv venv
source .venv/bin/activate
deactivate
```
Run and build
```
uv add -r requirements.txt
uv run main.py
```
```
uv build
ls dist/
```
```
uv lock
uv sync
```

Clone a privare repo (ssh url) and run locally using uv
```
git clone git@github.com:mir-owahed/bg-remover.git
cd bg-remover/
code .
uv lock
uv sync
uv run main.py

```
```
ubuntu@ip-10-0-0-122:/python-app$ 
   34  mkdir python-app
   35  sudo mkdir python-app
   36  cd python-app/
   37  nano app.py
   38  sudo nano app.py
   39  sudo nano requirements.txt
   40  pip3 install -r requirements.txt 
   41  sudo pip3 install -r requirements.txt 
   42  pip3 install flask
   43  sudo pip3 install flask
```
```
91  python3 app.py
   92  pip install flsk
   93  pip install flask
   94  python3 app.py
   95  pip install pillow
   96  python3 app.py
   97  pip install rembg
   98  python3 app.py
   99  pip install onnxruntime
  100  python3 app.py
  101  /bin/python3 /home/mir/.vscode/extensions/ms-python.python-2025.2.0-linux-x64/python_files/printEnvVariablesToFile.py /home/mir/.vscode/extensions/ms-python.python-2025.2.0-linux-x64/python_files/deactivate/bash/envVars.txt
```

