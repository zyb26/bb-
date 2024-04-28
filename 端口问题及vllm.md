# 大模型 --> http://127.0.0.1:9002/v1 --> vllm 0.0.0.0 接收

大模型和LLM接口不适配 --> 转换为OpenAI的接口调用方式
生成Token_id 然后放入大模型 转换为句子 

# 首先需要创建python环境3.11
然后vllm release 安装 <-- 直接 pip install vllm
# 1.切换到环境
# 2. 写server.sh
#!/bin/bash

python -m vllm.entrypoints.openai.api_server \
    --dtype float16 \
    --served-model-name qwen1half-7b-chat \  # 不用改 要和代码里的.env对应
    --model /home/admin/workspace/models/Qwen1.5-7B-Chat \  # 模型路径
    --tensor-parallel-size 1 \
    --max-model-len 10000 \
    --host 0.0.0.0 \
    --port 9002 \

# VLLM启动URL
api_base = http://127.0.0.1:9002/v1
temperature = 0
max_tokens = 1000

# 这样子服务器的地址就会被这个vllm接收
# !!!如何把服务器的地址映射到本地，来使得本地(连接服务器的电脑)的地址也可以被vllm接受
本地的端口和服务器的端口连接 本地也可以使用api_base = http://127.0.0.1:9002/v1



# 3. bash server.sh  --> 


# Ngrok内网穿透工具
下载并安装Ngrok客户端。
    在终端中输入命令ngrokauthtoken[auth_token]，将auth_token替换为您的Ngrok授权令牌。
    在终端中输入命令ngrokhttp[port]，将port替换为您要公开的本地服务端口。
    Ngrok会为您提供一个公网URL，您可以通过此URL访问您的本地服务。



# 一、部署到服务器上
# 1. 先在服务器上面起一个0.0.0.0 的接收端口 端口号8000
# 2. 通过vscode 下方的端口来和自己本机的端口进行交互(自己本机的接口就可以使用127.0.0.1:8000了) 

# 二、部署到外部平台上（内网击穿）
# 1. 先起一个接收的0.0.0.0的接收端口 端口号8000
# 2. 对于这个接收端口进行内网击穿 Ngrok 会把这个 返回一个外部web网址来供我们调用
