# ShreyAI

I always wanted to create my own AI and use my own alexa. However, the I wist there was one central place with all the information which is why i am creating this. 
I am doing all of this using a gaming pc  with a 3060ti

Open windows powershell and type 

```
wsl --install -d Ubuntu-22.04

mkdir whisperdata

 docker run -itd -p 10300:10300 -v ~/whisperdata/:/data rhasspy/wyoming-whisper \          --model tiny-int8 --language en

mkdir piperdata

shreyas@DESKTOP-UAJDFOE:~$ docker run -itd -p 10200:10200 -v ~/piperdata/:/data rhasspy/wyoming-piper \
    --voice en_US-lessac-medium


 sudo docker ps

git clone https://github.com/rhasspy/piper-recording-studio.git

 cd piper-recording-studio
 sudo apt install python3.10-venv
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install --upgrade pip
 python3 -m pip install -r requirements.txt
python3 -m piper_recording_studio
```
