## Continous monitoring with prometheus and grafana

### Set up virtual environment
```
python -m venv loan_env
source loan_env/bin/activate

pip install -r requirements.txt
pip install .
```

### CORSMIDDLEWARE
- cross origin Resource sharing refers to a situation whwn a frontend running in a browser has a javascript code that communicates with a backend in with a different "origin " that itself.

- Hence the need to specify origins,methods or headers in order for browsers to be permitted to usse them.