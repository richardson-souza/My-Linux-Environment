## My Linux Environment
### Meu Ambiente Linux

Setup and software of my personal laptop, powered by [Ubuntu Linux 18.04](https://ubuntu.com/download/desktop).  

## First Update
### Primeira atualização

This is the first thing you should do after fresh installing Ubuntu  
Essa é a primeira coisa a fazer após uma instalação nova

```bash
$ sudo apt update && sudo apt upgrade
```

## Enable Canonical Partners repo
### Habilitar repositório de parceiros

```bash
$ sudo sed -i 's/# deb http/deb http/g' /etc/apt/sources.list
$ sudo apt update
```

## Install Build Essential, Python-setuptools and Python-dev

```bash
$ sudo apt install build-essential python-setuptools python-dev python3-distutils
```

## Install Media Codecs
### Instalar pacotes multimídia

```bash
$ sudo apt install ubuntu-restricted-extras
```

## Enable 'Minimize on Click' for the Ubuntu Dock
### Habilitar 'Minimizar ao clicar' para o Ubuntu Dock

```bash
$ gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'
```

## Gnome Tweaks and Show/Hide All Hidden Startup Applications
### Mostar aplicações ocultas que iniciam com o sistema

```bash
$ sudo apt install gnome-tweaks
$ sudo sed -i 's/NoDisplay=true/NoDisplay=false/g' /etc/xdg/autostart/*.desktop
```
## Curl

```bash
$ sudo apt install curl
```

## OpenJDK 8
```bash
$ sudo apt-get install openjdk-8-*
```

## Node  

```bash
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
$ source ~/.bashrc
$ nvm install node
```  

## IONIC

```bash 
$ npm install -g @ionic/cli
$ ionic start myApp tabs
$ cd myApp/
$ ionic serve
```  
If it works smoothly continue to build on Android device  
Se tudo funcionar pode continuar para fazer build em dispositivos Android

### Build on device

```bash 
$ sudo apt install adb
```  
Open the file:

```bash 
$ vim ~/.bashrc
```  
Add in the end of file:  
ANDROID_SDK_ROOT=/home/rsouza/Android/Sdk  
PATH=${PATH}:$ANDROID_SDK_ROOT/tools:$ANDROID_SDK_ROOT/platform-tools:$ANDROID_SDK_ROOT/build-tools

![android](img03.png) 

Save, exit and continue:

```bash 
$ source ~/.bashrc
$ curl -s "https://get.sdkman.io" | bash
$ source ~/.bashrc
$ sdk version
$ sdk install gradle 5.0
```  

Now, inside de project execute:

```bash 
$ ionic cordova run android --device
```  

## Install Docker  
### Instalar docker

```bash 
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
$ sudo usermod -aG docker $USER

Reiniciar
Restart 
$ sudo shutdown -r now
``` 
## Install Docker Compose
### Instalar docker compose

```bash
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
$ docker-compose --version
```

## Install CUDA 11.1
### Instalar CUDA 11.1
```bash
The base installer is available for download below  
A instalação base esta disponível abaixo  
$ wget https://developer.download.nvidia.com/compute/cuda/11.1.0/local_installers/cuda_11.1.0_455.23.05_linux.run

Switch to tty3 by pressing Ctl+Alt+F3  
Mude pata tt3 (Crtl+Alt+F3)

Isolate multi-user.target  
Isole multi-user.target  
$ sudo systemctl isolate multi-user.target

Note that nvidia-drm is currently in use  
Veja que nvidia-drm ainda esta em uso  
$ lsmod | grep nvidia.drm

Unload nvidia-drm  
$ sudo modprobe -r nvidia-drm

nvidia-drm is not in use anymore  
nvidia-drm não está mais em uso  
$ lsmod | grep nvidia.drm  

Go to your download folder and run the cuda installation  
Vá até o local do dowload e execute o arquivo de instalação  
$ sudo bash cuda_11.1.0_455.23.05_linux.run  

When installation has finished, confirm that the CUDA Version has been updated  
Quando a instalação terminar, confirme se a versão do CUDA foi atualizada  
$ nvidia-smi  

Start the GUI again  
Inicie novamente o modo gráfico  
$ sudo systemctl start graphical.target  

Open the file ".bashrc" by running
Abra o arquivo ".bashrc" executando  
$ sudo vim ~/.bashrc  

Add the following lines at the end of the file  
Adicione as linhas abaixo ao final do arquivo  

#set PATH for cuda 11.1 installation
if [ -d "/usr/local/cuda-11.1/bin/" ]; then
    export PATH=/usr/local/cuda-11.1/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda-11.1/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
fi  

Reload the file ".bashrc"  
Recarregue o arquivo ".bashrc"  
$ source ~/.bashrc  

Check the versions for the installation  
Verifique a versão instalada
$ nvcc --version
```

## Start a TensorFlow Docker container
### Iniciar Tensorflow com Docker

```bash

Setup the stable repository and the GPG key  
Incluir um repositório estável

$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
$ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
$ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
$ sudo apt-get update
$ sudo apt-get install -y nvidia-docker2
$ sudo systemctl restart docker

Check instalation  
Verifique a instalação  
$ docker run --rm --gpus all nvidia/cuda:11.1-base nvidia-smi

Example using CPU-only images  
Exemplo usando apenad imagens com suporte a CPU
$ docker run -it --rm tensorflow/tensorflow \
     python -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"

Verify your nvidia-docker installation  
Verifique a instalação do nvidia-docker
$ docker run --gpus all --rm nvidia/cuda nvidia-smi

Example using GPU-enabled image  
Exemplo usando imagens com suporte a GPU  
$ docker run --gpus all -it --rm tensorflow/tensorflow:latest-gpu \
     python -c "import tensorflow as tf; print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```

### Spotify  

```bash 
$ curl -sS https://download.spotify.com/debian/pubkey.gpg | sudo apt-key add -
$ echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
$ sudo apt-get update && sudo apt-get install spotify-client
``` 

Restart the system.  

## Acknowledgments

[OMG Ubuntu](https://www.omgubuntu.co.uk/2018/04/things-to-do-after-installing-ubuntu-18-04)  
[NVM](https://github.com/creationix/nvm)  
[IONIC](https://ionicframework.com/docs/intro/installation/)
[TENSORFLOW DOCKER](https://www.tensorflow.org/install/docker)
[NVIDIA_DOCKER](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#install-guide)
[DOCKER](https://docs.docker.com/engine/install/ubuntu/)
[DOCKER-COMPOSE](https://docs.docker.com/compose/install/)
 

