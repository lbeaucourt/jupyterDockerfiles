FROM ubuntu:16.04

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y locales
RUN locale-gen en_US en_US.UTF-8

# Install python packages 
RUN apt-get install -y python3

# Install compile tools
RUN apt-get update
RUN apt-get install -y python3-dev gfortran libatlas-base-dev libfreetype6-dev libxft-dev libpng-dev g++ make patch

# Install dependencies tools 
RUN apt-get install -y wget vim
RUN wget -O /tmp/get-pip.py https://bootstrap.pypa.io/get-pip.py
RUN python3 /tmp/get-pip.py
RUN apt-get install -y git
RUN pip install --upgrade pip

# Install jupyter notebook
RUN pip install -U notebook
RUN pip install --upgrade jupyter

#add dataframe display widget
RUN pip install -U autovizwidget && jupyter nbextension enable --py --sys-prefix widgetsnbextension

#extend jupyter to jupyterlab
#RUN pip install -U jupyterlab && jupyter serverextension enable --py jupyterlab --sys-prefix 

# python data core packages
RUN pip install -U numpy pandas cython joblib xlrd xlsxwriter networkx pyyaml

# python ml packages
RUN pip install -U scikit-learn xgboost prophet

# Install K-prototypes algo
RUN cd /usr/local/src && git clone https://github.com/nicodv/kmodes.git && cd kmodes && sed -i '20d' setup.py && python3 setup.py install

# Deep learning packages
RUN pip install -U tensorflow keras

# Install tensorflow models object detection
RUN git clone https://github.com/tensorflow/models /usr/local/lib/python3.5/dist-packages/tensorflow/models
RUN apt-get install -y python-pil python-lxml python-tk unzip

RUN cd /usr/local/lib/python3.5/dist-packages/tensorflow/models/research/ && wget -O protobuf.zip https://github.com/google/protobuf/releases/download/v3.0.0/protoc-3.0.0-linux-x86_64.zip && unzip protobuf.zip
RUN cd /usr/local/lib/python3.5/dist-packages/tensorflow/models/research/ && ./bin/protoc object_detection/protos/*.proto --python_out=.

#Set TF object detection available
ENV PYTHONPATH "$PYTHONPATH:/usr/local/lib/python3.5/dist-packages/tensorflow/models/research:/usr/local/lib/python3.5/dist-packages/tensorflow/models/research/slim"

# Image/video manipulation
RUN apt-get install -y ffmpeg graphviz
RUN pip install -U moviepy graphviz imutils

# Install OpenCV
RUN apt-get install -y cmake
RUN git clone https://github.com/opencv/opencv.git /usr/local/src/opencv
RUN cd /usr/local/src/opencv/ && mkdir build
RUN cd /usr/local/src/opencv/build && cmake -D CMAKE_INSTALL_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local/ .. && make -j4 && make install

# Database Driver
RUN pip install -U boto3 pymongo elasticsearch

# Install visualization tools 
RUN pip install -U matplotlib seaborn ggplot plotly cufflinks prettyplotlib mplleaflet pandoc

# Install Kaggle API
RUN pip install -U kaggle

#Setting up working directory 
RUN mkdir /lab
WORKDIR /lab

#Minimize image size 
RUN (apt-get autoremove -y; \
     apt-get autoclean -y)

#Setting up ipython notebook server 
EXPOSE 8888 
CMD jupyter notebook --no-browser --ip=0.0.0.0 --port 8888 --allow-root
