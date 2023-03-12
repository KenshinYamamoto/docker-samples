FROM ubuntu:latest

RUN apt update && apt install -y wget

WORKDIR /opt

# anacondaのインストーラを入れ、実行したのちにインストーラを削除
# rm -f で強制削除(force)
RUN wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh && \
    sh Anaconda3-2022.10-Linux-x86_64.sh -b -p /opt/anaconda3 && \
    rm -f Anaconda3-2022.10-Linux-x86_64.sh

# /opt/anaconda3/binのパスを通す($PATHに追加)
ENV PATH /opt/anaconda3/bin:$PATH

# Pythonに関するパッケージをインストール
RUN pip install --upgrade pip

WORKDIR /

# --ip=0.0.0.0でlocalhost
# --allow-rootでrootユーザでの実行許可
# --LabApp.tokenでjupyterLab起動時のトークン指定
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--allow-root", "--LabApp.token=''"]