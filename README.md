# Reducing_WAF_Flash

Flash-based solid state drives lack support for in-place updates, and hence deploy a flash translation layer to absorb the writes. For this purpose, SSDs
implement a log-structured storage system introducing garbage collection
and write amplification overheads. In this paper, we present a machine
learning based approach for reducing write amplification in log structured file
systems via death-time prediction of logical block addresses. We define
death-time of a data element as the number of I/O writes before which the
data element is overwritten. We leverage the sequential nature of I/O
accesses to train lightweight, yet powerful, temporal convolutional network
(TCN) based models to predict death times of logical blocks in SSDs. We
leverage the predicted death-times in designing ML-DT, a near-optimal data
placement technique that minimizes write amplification (WA) in log
structured storage systems. We compare our approach with three state-ofthe-
art data placement schemes and show that ML-DT achieves the lowest
WA by utilizing the learnt I/O death-time patterns from real-world storage
workloads. Our proposed approach results in up to 14% reduction in write
amplification compared to the best baseline technique. Additionally, we
present a mapping learning technique to test the applicability of our
approach to new or unseen workloads and present a hyper-parameter
sensitive study.



Required Libraries: (Please see a setup tutorial below)
Jupyter
Keras
Keras-tcn
Tensor flow-gpu
Pandas
Ipykernel



How to run:
Download the traces (See source links from paper)
Parse the traces to a data frame
Data prepare and pre-process the traces to add death time information
Use the data to train the model using the traces and generate predictions in a CSV file
Use the predictions to run the scripts (FTL_Greedy_v1, FTL_deathtime_v2, FTL_deathtime_v3)
Baselines used: AutoStream, WARCIP, DAC




Setup:

Install conda for Ubuntu: (If needed)
https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html

conda create -n “instance_name” python=3.7 (Replace “instance_name” with your desired name)
conda install tensorflow-gpu
pip install ipykernel
python -m ipykernel install --user --name gpu --display-name gpu (Replace “gpu” with your desired name)
conda install jupyter
pip install keras
conda install pandas
pip install sklearn
pip install matplotlib
pip install keras-tcn
jupyter notebook --generate-config

Add the following lines at the beginning of the config file:
c = get_config()
c.NotebookApp.ip = '*'
c.NotebookApp.open_browser = False
c.NotebookApp.port = 8888

Start Jupyter instance :
jupyter-notebook --no-browser --port=8888
