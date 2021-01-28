mkdir ./data
cd ./data
for input_size in 512 768 1024
do
  kaggle datasets download -d cdeotte/jpeg-melanoma-${input_size}x${input_size}
  unzip -q jpeg-melanoma-${input_size}x${input_size}.zip -d jpeg-melanoma-${input_size}x${input_size}
  rm jpeg-melanoma-${input_size}x${input_size}.zip 
done




 kaggle datasets download -d cdeotte/jpeg-isic2019-${input_size}x${input_size}
unzip -q jpeg-isic2019-${input_size}x${input_size}.zip -d jpeg-isic2019-${input_size}x${input_size}
jpeg-isic2019-${input_size}x${input_size}.zip

mkdir ./data
cd ./data

for input_size in 1024
do
  kaggle datasets download -d cdeotte/jpeg-isic2019-${input_size}x${input_size}
  unzip -q jpeg-isic2019-${input_size}x${input_size}.zip -d jpeg-isic2019-${input_size}x${input_size}
  rm jpeg-isic2019-${input_size}x${input_size}.zip
done


python train.py --kernel-type 9c_meta_b3_768_512_ext_18ep --data-dir ../data/ --data-folder 768 --image-size 512 --enet-type efficientnet_b3 --use-meta --n-epochs 18 --use-amp --CUDA_VISIBLE_DEVICES 0 --batch_size=32


python train.py --kernel-type 9c_b4ns_448_ext_15ep-newfold --data-dir ../data/ --data-folder 512 --image-size 448 --enet-type tf_efficientnet_b4_ns --use-amp --CUDA_VISIBLE_DEVICES 0 --batch_size=1

python train.py --kernel-type 9c_meta128_32_b5ns_384_ext_15ep --data-dir ./data/ --data-folder 512 --image-size 384 --enet-type tf_efficientnet_b5_ns --use-meta --n-meta-dim 128,32 --use-amp --CUDA_VISIBLE_DEVICES 0 --batch_size=1


python train.py --kernel-type 9c_meta128_32_b5ns_384_ext_15ep --data-dir ../data/ --data-folder 512 --image-size 128 --enet-type tf_efficientnet_b5_ns --use-meta --n-meta-dim 128,32 --use-amp --CUDA_VISIBLE_DEVICES 0 --batch_size=1

python train.py --kernel-type 9c_meta128_32_b5ns_384_ext_15ep --data-dir ../data/ --data-folder 512 --image-size 128 --enet-type tf_efficientnet_b5_ns --use-meta --n-meta-dim 128,32 --use-amp --CUDA_VISIBLE_DEVICES 0 --batch_size=64


sudo apt-get purge nvidia*
sudo apt-get autoremove
sudo apt-get autoclean
sudo rm -rf /usr/local/cuda-10.0

git clone https://github.com/NVIDIA/apex
cd apex
pip install -v --disable-pip-version-check --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" ./


sudo apt-get update  
sudo apt-get upgrade  
sudo apt-get install synaptic

git clone https://github.com/NVIDIA/apex
cd apex
pip install -v --disable-pip-version-check --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" ./

pip install -v --disable-pip-version-check --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" ./
pip install -v --disable-pip-version-check --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" ./


apt-get install software-properties-common

add-apt-repository ppa:jonathonf/gcc-7.1
apt-get update
apt-get install gcc-7 g++-7

add-apt-repository ppa:jonathonf/gcc-7.1
sudo apt-get update
sudo apt-get install gcc-7 g++-7

apt update -qq
apt install -yq software-properties-common
add-apt-repository -y ppa:ubuntu-toolchain-r/test
apt update -qq
sudo apt install -yq g++-7


distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
   && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
   && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
Note


curl https://get.docker.com | sh \
  && sudo systemctl start docker \
  && sudo systemctl enable docker


sudo apt update
sudo apt-get install -y nvidia-docker2



###docker run --gpus all --rm -itd --name papex -v $PWD:/workspace  jetrunner/pytorch-apex:release-1.4.0

docker run --ipc=host --gpus all --rm -itd --name papex -v $PWD:/workspace  jetrunner/pytorch-apex:release-1.4.0

https://github.com/ultralytics/yolov3/wiki/Docker-Quickstart


docker commit -a "jiahuigeng@rwth-aachen.de" -m "pytorch apex for cv" 4b2c0337afb6 papex:v1


docker run --ipc=host --gpus all --rm -itd --name rapex -v $PWD:/workspace  r9y9/pytorch-apex:1.4.0-cuda10.1-cudnn7-apex-devel


https://github.com/OpenMined/PySyft/blob/v0.2.5/examples/tutorials/advanced/websockets_mnist_parallel/Asynchronous-federated-learning-on-MNIST.ipynb


python train.py --kernel-type 9c_meta128_32_b5ns_384_ext_15ep --data-dir ../data/ --data-folder 512 --image-size 128 --enet-type tf_efficientnet_b5_ns --use-meta --n-meta-dim 128,32 --use-amp --CUDA_VISIBLE_DEVICES 0 --batch_size=64


python train.py --kernel-type 9c_meta128_32_b5ns_384_ext_15ep --data-dir ../data/ --data-folder 512 --image-size 64 --enet-type tf_efficientnet_b5_ns --use-meta --n-meta-dim 128,32 --use-amp --CUDA_VISIBLE_DEVICES 0 --batch_size=16 --model-dir weight0


python train.py --kernel-type 9c_meta128_32_b5ns_384_ext_15ep --data-dir ../data/ --data-folder 512 --image-size 64 --enet-type tf_efficientnet_b5_ns --use-meta --n-meta-dim 128,32 --use-amp --CUDA_VISIBLE_DEVICES 0 --batch_size=16 --model-dir weight1