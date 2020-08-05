FROM ubuntu:18.04

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y locales
RUN locale-gen en_US en_US.UTF-8

# Install python packages 
RUN apt-get install -y python3

# Install compile tools
RUN apt-get update
RUN apt-get install -y python3-dev gfortran libatlas-base-dev libfreetype6-dev libxft-dev libpng-dev g++ make patch lib32ncurses5-dev

# Install dependencies tools 
RUN apt-get install -y curl vim
RUN curl https://bootstrap.pypa.io/get-pip.py -o /tmp/get-pip.py
#RUN wget -O /tmp/get-pip.py https://bootstrap.pypa.io/get-pip.py
RUN python3 /tmp/get-pip.py
RUN apt-get install -y git
RUN pip install -U pip

# Install jupyter notebook
RUN pip install -U notebook
RUN pip install --upgrade jupyter

#add dataframe display widget
RUN pip install -U autovizwidget && jupyter nbextension enable --py --sys-prefix widgetsnbextension

#extend jupyter to jupyterlab
#RUN pip install -U jupyterlab && jupyter serverextension enable --py jupyterlab --sys-prefix 

# python data core packages
RUN pip install -U numpy pandas cython joblib xlrd xlsxwriter networkx pyyaml pandas-profiling[notebook]

# python ml packages
RUN pip install -U scikit-learn xgboost

# Install K-prototypes algo
RUN cd /usr/local/src && git clone https://github.com/nicodv/kmodes.git && cd kmodes && sed -i '20d' setup.py && python3 setup.py install

# Database Driver
RUN pip install -U boto3 pymongo elasticsearch

# Install visualization tools 
RUN pip install -U matplotlib seaborn ggplot plotly prettyplotlib mplleaflet pandoc

#Setting up working directory 
RUN mkdir /lab
WORKDIR /lab

#Minimize image size 
RUN (apt-get autoremove -y; \
     apt-get autoclean -y)

#Setting up ipython notebook server 
EXPOSE 8888 
CMD jupyter notebook --no-browser --ip=0.0.0.0 --port 8888 --allow-root
