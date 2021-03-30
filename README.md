# Continuous Learning Platform (CLP)

The main aim of the **Continuous Learning Platform (CLP)** is to make available a large amount of labeled inertial signals related of ADLs and falls, from existing datasets or applications. Labeled inertial signals can be used by researches to both validate new ADLs recognition techniques. Activity recognition models can be integrated into existing domain dependent applications that require ADLs recognition in order to provide application functionalities (e.g., estimation of energy expenditure, monitoring the development of the Parkinson's disease, and early detection of dementia).
To achieve the aim, CLP collects inertial signal from existing datasets, manage these data and finally uniforms them, obtaining a single final dataset.

The CLP platform works in four main phases: 
- the **Import phase** provides the acquisition of an existing dataset and to standardize the organization and the representation of the imported data; 
- the **Data Uniformation** phase takes care of bringing the data to have the same unit of measurement and a common representation interval; 
- the **Feature Extraction** phase is responsible for calculating a set of features that analyze the characteristics of the uniform data; 
- the **Labels Uniformation** phase allows to standardize the data on the basis of the labels they represent.


## Implementation

We have decided to create different components designed and built to be independent from each other.

[<img src="/architecture.png" width="450"/>](/architecture.png)


The components are:

- **[Data Collection](https://gitlab.com/Pervasive-Healthcare/CLP-DataCollection)** which provides to upload your own dataset into the database made available by the platform; 

- **[Data Management](https://gitlab.com/Pervasive-Healthcare/CLP-DataManagement)** that deals with standardizing heterogeneous datasets in a single homogeneous database; 

- **[Data Distribution](https://gitlab.com/Pervasive-Healthcare/CLP-DataDistribution)** which provides the sets of signals labelled according to specific needs, the trained classifiers and the labels corresponding to activities from the signals; 

- **[Repository Manager](https://gitlab.com/Pervasive-Healthcare/CLP_RepositoryManagement/)** that deals with the management and storage of all platform data.

For the platform, we collected several datasets and developed, for each one, the drivers to load them in the platform. They are available in the following repository: [CLP Datasets](https://gitlab.com/Pervasive-Healthcare/clp_datasets)


## Code

### Prerequisites
- [Python](https://www.python.org/) 3.8
- [MongoDB*](https://www.mongodb.com/it) 4.2.0
- [RabbitMQ*](https://www.rabbitmq.com/download.html) 3.8.9
- [MATLAB](https://it.mathworks.com/products/matlab.html?s_tid=hp_products_matlab) R2020b

### *(Alternative)
You can avoid to install MongoDB and RabbitMQ, using Docker launching the command:
```
  docker-compose up
```
An example of the 'docker-compose.yml' file is:
```
version: '3.3' 
services:
    db:
        image: mongo 
        ports:
            - "27017:27017"

    rabbitmq:
        image: rabbitmq:3.8-management
        container_name: rabbitmq 
        environment:
            RABBITMQ_DEFAULT_USER: rabbitmq 
            RABBITMQ_DEFAULT_PASS: rabbitmq 
            RABBITMQ_LISTENER_PORT: 15672 
            RABBITMQ_LISTENER_SSL: "false" 
            RABBITMQ_DISTRIBUTION_BUFFER_SIZE: 512000
        ports:
            - 5672:5672
            - 15672:15672
```

### Installation

1. RabbitMQ: create a new user (credentials, **rabbitmq:rabbitmq**) with all permissions. You can create it using the GUI interface at http://localhost:15672/ (note that you need to abilitate it, https://www.rabbitmq.com/management.html#getting-started).

2. MATLAB: install the packages:  **[Signal Processing Toolbox](https://it.mathworks.com/products/signal.html)** and **[Statistics and Machine Learning Toolbox](https://it.mathworks.com/help/stats/index.html?s_tid=CRUX_lftnav)**.

3. Python: install **[MATLAB Engine API for Python](https://it.mathworks.com/help/matlab/matlab_external/install-the-matlab-engine-for-python.html)**.

3. Python: install required [dependencies](/requirements.txt).

4. (Optionally) Download [mongoDB Compass](https://www.mongodb.com/products/compass) to visualize and work with data through an intuitive GUI.


### Usage

Once that everything is installed and is running correctly, launch each component in a different terminal with the command:
```
python main.py
```
For convenience you can use [Visual Studio Code](https://code.visualstudio.com/), which allows to keep multiple terminals simultaneously.


## Citation
If you use this code for your research, please consider citing:

```
  @inproceedings{Ferrari2019AFF,
      title={A Framework for Long-Term Data Collection to Support Automatic Human Activity Recognition},
      author={A. Ferrari and D. Micucci and M. Mobilio and P. Napoletano},
      booktitle={Intelligent Environments},
      year={2019}
  }
```
