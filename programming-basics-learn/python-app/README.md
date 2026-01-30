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
uv add flask
uv remove flask
uv run main.py
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
uv cache clean
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
## Write API using fastapi
## FastAPI project setup using 'uv'
```
```
mkdir fastapi-project
cd fastapi-project/
code .
mir@DESKTOP-JASRD4A:~/fastapi-project$ uv init
Initialized project `fastapi-project`
mir@DESKTOP-JASRD4A:~/fastapi-project$ uv venv
Using CPython 3.12.3 interpreter at: /usr/bin/python3.12
Creating virtual environment at: .venv
Activate with: source .venv/bin/activate
mir@DESKTOP-JASRD4A:~/fastapi-project$ source .venv/bin/activate
(fastapi-project) mir@DESKTOP-JASRD4A:~/fastapi-project$ uv pip install "fastapi[standard]"
or
uv pip install -r requirements.txt
(fastapi-project) mir@DESKTOP-JASRD4A:~/fastapi-project$ uv run fastapi dev main.py

```
access docs from browser
```
http://localhost:8000/docs
http://localhost:8000/redoc
```
```
curl http://localhost:8000/
```

```
Ref: <https://fastapi.tiangolo.com/tutorial/first-steps/>
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
```
git --version
 1994  git clone https://github.com/mir-owahed/python-flask-app.git
 1995  cd python-flask-app/
 1996  code .
 1997  python3 --version
 1998  python --version
 1999  python3 -m venv .venv
 2000  source .venv/bin/activate
 2001  pip3 --version
 2002  python -m pip install --upgrade pip
 2003  pip3 --version
 2004  pip install "fastapi[standard]"
 2005  fastapi dev main.py
 2006  history
```
How to run python app
```
```
 git clone https://github.com/iam-veeramalla/hello-world-mlops.git
 2000  cd hello-world-mlops/
 2001  code .
python3 -m venv .venv
 2001  source .venv/bin/activate
 2002  which python
 2003  python3 --version
 2004  pip install -r requirements.txt 
 2005  python3 train.py
 2006  ls artifacts/
 2007  python3 run_model.py --input "[5, 10, 3, 2]"
 2008  python3 run_model.py --input "[1, 1, 1, 1]"
 python3 app.py
 curl -X POST "http://127.0.0.1:5001/predict" -H "Content-Type: application/json" -d '{"f
eatures":[5.1,3.5,1.4,0.2]}'
 2009  history
 ```
```

