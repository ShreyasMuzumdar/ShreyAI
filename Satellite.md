```
sudo apt-get update
```
```
sudo apt-get upgrade
```

```
sudo apt-get install --no-install-recommends git python3-venv
```
cd wyoming-satellite/
python3 -m venv .venv
.venv/bin/pip3 install --upgrade pip
.venv/bin/pip3 install --upgrade wheel setuptools
.venv/bin/pip3 install \
  -f 'https://synesthesiam.github.io/prebuilt-apps/' \
  -e '.[all]'
