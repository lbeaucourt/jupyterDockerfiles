# Docker image: python jupyter notebooks for Data Science

See env.txt for each folders


### Jupyter Calliope:

Energy grid modelisation framework

### Jupyter Python CPLEX:

Python with Networks and DOCPLEX library
(need to add CPLEX bin file in folder)


### Jupyter Python:

Python with standard Data & ML librairies

### Jupyter PythonCV:

Python for computer vision application (OpendCV) and Deep-Learning packages

### Jupyter PythonDL:

Python for Deep-Learning

### Jupyter PythonFull: (Shall be rename)

Full python for ML and NLP application (include Google query)

### Jupyter PythonGeo:

Python librairies for geodata manipulation

### Jupyter PythonLite:

Lite python librairies for ML


## How to use:

- Install docker

- (build docker) docker build -t NAME .

- (run docker)   docker run -m 8GB -it --rm -p 8888:8888 -v YOUR_FOLDER:/lab NAME