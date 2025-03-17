# ShreyAI

I always wanted to create my own AI and use my own alexa. However, the I wist there was one central place with all the information which is why i am creating this. 
I am doing all of this using a gaming pc  with a 3060ti

Open windows powershell and type 

```
wsl --install -d Ubuntu-22.04

mkdir whisperdata

 sudo  docker run -it -p 10300:10300 -v ~/whisperdata/:/data rhasspy/wyoming-whisper \
     --model tiny-int8 --language en
mkdir piperdata

sudo docker run -itd -p 10200:10200 -v ~/piperdata/:/data rhasspy/wyoming-piper \
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



cd /output/en-US/
cd .chat

sudo apt install ffmpeg

cd ../../../

pip install numpy
pip install onnxruntime
 python3 -m export_dataset ~/piper-recording-studio/output/en-US/ ~/my-voice-dataset
deactivate

exit the tab and reenter

## Make a new directory for training

mkdir training
cd training

## Clone the Piper Repo

git clone https://github.com/rhasspy/piper.git

## Create another python virtual environment and activate it

python3 -m venv .venv
source .venv/bin/activate

python3 -m pip install pip==23.3.1

pip install numpy==1.24.4

pip install torchmetrics==0.11.4

cd piper/src/python
python3 -m pip install --upgrade wheel setuptools
pip3 install -e .

pip install pytorch-lightning==1.7.0 torch==1.11.0

sudo apt-get update
 sudo apt-get install build-essential
sudo apt-get install python3-dev

./build_monotonic_align.sh

python3 -m piper_train.preprocess \
  --language en \
  --input-dir ~/my-voice-dataset/ \
  --output-dir ~/training/train-me \
  --dataset-format ljspeech \
  --single-speaker \
  --sample-rate 22050


wget https://huggingface.co/datasets/rhasspy/piper-checkpoints/resolve/main/en/en_US/lessac/medium/epoch%3D2164-step%3D1355540.ckpt

pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu116
sudo apt install nvidia-cuda-toolkit
python3 -m piper_train \
    --dataset-dir ~/training/train-me \
    --accelerator 'gpu' \
    --devices 1 \
    --batch-size 16 \
    --validation-split 0.0 \
    --num-test-examples 0 \
    --max_epochs 6000 \
    --resume_from_checkpoint "~/training/piper/src/python/epoch=2164-step=1355540.ckpt" \
    --checkpoint-epochs 1 \
    --precision 16 \
    --max-phoneme-ids 400 \
    --quality medium \
    --log_every_n_steps 1

python3 -m piper_train.export_onnx \
    "/home/shreyas/training/train-me/lightning_logs/version_7/checkpoints/epoch=11999-step=1670260.ckpt" \
    ~/training/model.onnx
```
