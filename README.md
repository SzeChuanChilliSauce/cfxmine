# cfxmine

A C++ miner for Conflux PoW.

For detailed mining instructionn, please refer to [Conflux Tethys GPU Mining Instruction](https://forum.conflux.fun/t/topic/3775).

## 依赖（Dependencies）

```bash
1. 安装boost 1.65（不赘述）
	
2. 安装cuda（ubuntu 18.04）
    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
    sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
    wget https://developer.download.nvidia.com/compute/cuda/11.1.0/local_installers/cuda-repo-ubuntu1804-11-1-local_11.1.0-455.23.05-1_amd64.deb
    sudo dpkg -i cuda-repo-ubuntu1804-11-1-local_11.1.0-455.23.05-1_amd64.deb
    sudo apt-key add /var/cuda-repo-ubuntu1804-11-1-local/7fa2af80.pub
    sudo apt-get update
    sudo apt-get -y install cuda

3. 修改CMakeList.txt
    加入如下语句：
    # 设置BOOST_ROOT变量（boost根目录）
    set(BOOST_ROOT /usr/local/inlucde/boost)
    # cuda头文件目录
    include_directories(/usr/local/cuda/include)
    # 链接cuda库目录
    link_directories(/usr/local/cuda/lib64)
	
```

## 编译（Build）

`cfxmine` depends on  (version 3.18 or higher), and Boost (version 1.65.1).

On Linux, run the following command in a shell to build.

```bash
git clone https://github.com/SzeChuanChilliSauce/cfxmine.git
cd cfxmine
mkdir build && cd build
cmake -DCMAKE_B_TYPE=Release ..
make
```

On Windows, alternatively run:

```bash
mkdir build
cd build
cmake -A x64 -DCMAKE_BUILD_TYPE=Release ..
make
```

## 运行（Run）

cfxmine works with [Conflux-Rust](https://github.com/Conflux-Chain/conflux-rust) together. In order to run cfxmine, here are the steps:

1. Start Conflux-Rust with stratum enabled. In the configuration file, set
``mining_type = "stratum"``. By default, it will open 32525 port at the public address
of the client. You can also change the port in the configuration file.

2. Run ``./build/bin/cfxmine --addr A.B.C.D --port 32525 --gpu``, where ``A.B.C.D`` is the
public ip address of the client.

# cfxmine
A C++ miner for Conflux PoW.  
For detailed mining instruction, please refer to [Conflux Tethys GPU Mining Instruction](https://forum.conflux.fun/t/topic/3775).  

