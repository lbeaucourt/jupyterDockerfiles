FROM ubuntu:16.04

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y locales
RUN locale-gen en_US en_US.UTF-8

# Install python packages 
RUN apt-get install -y python3

# Install compile tools 
RUN apt-get update
RUN apt-get install -y build-essential cmake libboost-dev libexpat1-dev zlib1g-dev libbz2-dev \
    python3-dev gfortran libatlas-base-dev libfreetype6-dev libxft-dev libpng-dev g++ make patch lib32ncurses5-dev

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
#RUN  pip install -U jupyterlab && jupyter serverextension enable --py jupyterlab --sys-prefix 

# python data core packages 
RUN pip install -U numpy pandas scipy

# Install visualization tools 
RUN pip install -U matplotlib seaborn ggplot plotly==3.3 prettyplotlib mplleaflet pandoc

# Install geodata manipulation
RUN pip install -U pyshp shapely folium geojsoncontour geopandas osmium

# Install GDAL
#RUN apt-add-repository ppa:ubuntugis/ppa && apt-get update
#RUN apt-get update
RUN apt-get -y install libgdal1i libgdal1-dev libgdal-dev
#ENV CPLUS_INCLUDE_PATH=/usr/include/gdal
#ENV C_INCLUDE_PATH=/usr/include/gdal
RUN pip install pygdal==1.11.3.3

#Setting up working directory 
RUN mkdir /lab
WORKDIR /lab

#Minimize image size 
RUN (apt-get autoremove -y; \
     apt-get autoclean -y)

#Setting up ipython notebook server 
EXPOSE 8888 
CMD jupyter notebook --no-browser --ip=0.0.0.0 --port 8888 --allow-root
