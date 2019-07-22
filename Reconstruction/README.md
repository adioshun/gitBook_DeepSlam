# 3d reconstruction

---


- [Quick Steps](https://github.com/FusionEye/3d-reconstruction)


도커 파일 
```
FROM leontius/ubuntu-desktop-lxde-vnc:ros

# Switch to ROOT
USER root

RUN mkdir -p /root/Desktop && \
    cd /root/Desktop && \
    wget https://github.com/FusionEye/3d-reconstruction/archive/master.zip && \
    unzip master.zip && \
    rm master.zip

RUN pip2 install opencv-python==3.4.3.18 -i https://pypi.tuna.tsinghua.edu.cn/simple
RUN pip2 install Pillow==5.2.0 -i https://pypi.tuna.tsinghua.edu.cn/simple
```