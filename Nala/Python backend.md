### Levantar proyecto
Despues de clonar el proyecto vamos a la ruta del proyecto e instalamos las dependencias, en caso que este en la carpeta Nala, seria asi.
```bash
cd /Users/oscar/Desktop/Nala/backend_pyapi

python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```
Crea una carpeta llamada .local
```bash
mkdir .local
```
En ella crea el archivo pyapi_tunnel_config.json y pon lo siguiente
```json
{

"staging": {

"PG_UN": "backofficer",

"PG_DB_NAME": "postgres",

"PG_DB_PW": "nalaqG4bzDoe_",

"SSH_PKEY": "/Users/oscar/.ssh/id_ed25519",

"SSH_USERNAME": "ubuntu",

"SSH_HOST": "back.nala.rocks",

"SSH_PORT": 24,

"DB_HOST": "staging-nala-encrypted.chbcyhrn7a08.us-east-2.rds.amazonaws.com",

"DB_PORT": 5432,

"PORT": 5432,

"runtime": {

"HOST": "staging.api.nalarocks.com",

"LOCAL_URL": "https://staging.api.nalarocks.com"

}

}

}
```
y para levantar el proyecto toca ejecutar
```bash
python _scripts/run_local_pyapi_with_tunnel.py \
  --env staging \
  --config .local/pyapi_tunnel_config.json \
  --app-host 127.0.0.1 \
  --app-port 5000
```