# Docker image: python jupyter notebooks for Data Science

See env.txt for each folders


### Jupyter Calliope:

Energy grid modelisation framework

### Jupyter Python:

Python with standard Data & ML librairies

### Jupyter PythonCV:

Python for computer vision application (OpendCV) and Deep-Learning packages

### Jupyter PythonDL:

Python for Deep-Learning

### Jupyter PythonFull: (Shall be rename)

Full python for ML and NLP application (include Google query)

### Jupyter PythonLite:

Lite python librairies for ML



## How to use:

- Install docker

- (build docker) docker build -t jupyter-<version> .

- (run docker)   docker run -m 8GB -it --rm -p 8888:8888 -v /home/leo/Documents/:/lab jupyter<version>