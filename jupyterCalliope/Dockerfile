FROM ubuntu:18.04

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y locales
RUN locale-gen en_US en_US.UTF-8

# Install python packages
RUN apt-get install -y python3

# Install compile tools
RUN apt-get update
RUN apt-get install -y curl python3-dev gfortran libatlas-base-dev libfreetype6-dev libxft-dev libpng-dev g++ make patch lib32ncurses5-dev

# Install dependencies tools 
RUN apt-get install -y wget vim
RUN wget -O /tmp/get-pip.py https://bootstrap.pypa.io/get-pip.py
RUN python3 /tmp/get-pip.py
RUN apt-get install -y git
RUN pip install --upgrade pip

# Install conda
RUN apt-get update --fix-missing && \
    apt-get install -y wget bzip2 ca-certificates libglib2.0-0 libxext6 libsm6 libxrender1 git mercurial subversion && \
    apt-get clean

RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-4.7.12-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    /opt/conda/bin/conda clean -tipsy && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc && \
    find /opt/conda/ -follow -type f -name '*.a' -delete && \
    find /opt/conda/ -follow -type f -name '*.js.map' -delete && \
    /opt/conda/bin/conda clean -afy
RUN conda update -n base -c defaults conda

# Install caliope required packages
RUN conda install -c conda-forge pyomo
RUN conda install -c conda-forge ipopt coincbc glpk
RUN pip install -U jinja2 natsort netcdf4 numexpr pytest pytest-cov pytest-xdist xarray ruamel.yaml==0.16.5
RUN cd /usr/local/src && git clone https://github.com/calliope-project/calliope && cd calliope && sed -i '20d' setup.py && python3 setup.py install

# Install jupyter notebook
RUN pip install -U notebook
RUN pip install --upgrade jupyter

#add dataframe display widget
RUN pip install -U autovizwidget && jupyter nbextension enable --py --sys-prefix widgetsnbextension

# python data core packages
RUN pip install -U numpy pandas cython joblib xlrd xlsxwriter networkx pyyaml

# python ml packages
RUN pip install -U scikit-learn xgboost prophet

# Install K-prototypes algo
RUN cd /usr/local/src && git clone https://github.com/nicodv/kmodes.git && cd kmodes && sed -i '20d' setup.py && python3 setup.py install

# Database Driver
RUN pip install -U boto3 pymongo elasticsearch

# Install visualization tools 
RUN pip install -U matplotlib seaborn ggplot plotly==3.3 prettyplotlib mplleaflet pandoc

#Setting up working directory 
RUN mkdir /lab
WORKDIR /lab

#Minimize image size 
RUN (apt-get autoremove -y; \
     apt-get autoclean -y)

#Setting up ipython notebook server 
EXPOSE 8888 
CMD jupyter notebook --no-browser --ip=0.0.0.0 --port 8888 --allow-root
