# Install Google Assistant on Raspberry Pi

## Setup Google Assistant Api 
https://www.hackster.io/Salmanfarisvp/googlepi-google-assistant-on-raspberry-pi-9f3677

## Setup Enviroment 

```bash
sudo apt install python3-dev python3-venv portaudio19-dev libffi-dev libssl-dev -y

python3 -m venv env
env/bin/pip install setuptools --upgrade
source env/bin/activate
python -m pip install google-assistant-sdk[samples]
pip install --upgrade google-auth-oauthlib[tool]


```

### Authentificate with oauth file from google cloud
```bash
google-oauthlib-tool --client-secrets path/to/client_secret_XXXXX.json --scope https://www.googleapis.com/auth/assistant-sdk-prototype --save --headless

```
### Run example

```bash
python -m googlesamples.assistant.grpc.pushtotalk

```