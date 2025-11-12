# ===== 基础镜像 =====
FROM runpod/pytorch:2.4.0-py3.11-cuda12.4.1-devel-ubuntu22.04

# ===== 升级 pip、setuptools、wheel =====
RUN python3 -m pip install --upgrade pip setuptools wheel


# ===== 安装 git（comfy-cli 有时需要从 GitHub 拉包） =====
RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

# ===== 安装 comfy-cli =====
RUN python3 -m pip install --no-cache-dir --upgrade comfy-cli

# ===== 安装运行时依赖 =====
RUN python3 -m pip install --no-cache-dir runpod requests

# ===== 拷贝代码 =====
COPY rp_handler.py /rp_handler.py
COPY start.sh /start.sh
RUN chmod +x /rp_handler.py

# ===== 处理脚本换行符并授权执行 =====
RUN apt-get update && apt-get install -y dos2unix && rm -rf /var/lib/apt/lists/*
RUN dos2unix /start.sh && chmod +x /start.sh

# ===== 启动入口 =====
ENTRYPOINT ["/start.sh"]
