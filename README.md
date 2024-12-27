#### Course:

LA01 - Data Mining



#### Primary Instructor:

NICHOLAUS HENDRIK JEREMY, S.Kom., M.Kom.



#### Team Members:

ADHITYA SUSANTO

ANDREW ALDRICH LEE

FELIX OCTAVIUS XU

VINCENT OLIVER LIMARUS

#### Description
This project aims to find patterns in retail product purchases using frequent pattern mining. This method is one of the ways of conducting market basket analysis to gain valuable insights on customer purchases. The patterns found can then be used to compile discount bundles, reposition shelf items, or preemptive product restocks, depending on the preferred strategy.


We used 3 tools. Firstly, we used was the python mlxtend library which provides frequent pattern mining algorithms such as Apriori, FP-Growth, and H-Mine. The mlxtend frequent pattern algorithms accepts data in one-hot encoded format:


         P001 P002 P003 P004 P005

    T001 1    1    0     0    0 

    T002 1    0    1     0    1


Due to the sheer amount of data and the additional redundancy required in a one-hot encoded format, we had to scale down the dataset to 1.5% the original size for one-hot encoding. Even when scaled down, only the Apriori (with low_memory=True parameter) and H-Mine algorithms managed to work whereas the FP-Growth algorithm failed due to memory overload.


We then resided to a software we were learning about in our lab module, which was RapidMiner. RapidMiner provided us with FP-Growth algorithm and managed to process the entire dataset in a transaction-product format:


    T001 : P001

    T001 : P002

    T002 : P001

    T002 : P003

    T002 : P005


But because we needed at least 3 algorithms (the project's requirement), we searched for other alternatives and stumbled upon PAMI, a python library dedicated to pattern mining. It provided a vast variety of pattern mining algorithms for mining transactional, time-series, or even georeferenced data. PAMI is more efficient in processing the dataset because it uses a sparse dataframe format:


    T001 : P001, P002

    T002 : P001, P003, P005


While using it though, we have to admit it wasn't as easy to use as mlxtend or RapidMiner. We had to export the transformed dataset to a csv before feeding it back to the PAMI algorithms because the algorithm had trouble reading the dataframe itself, and the data separators had to be tab ('/t') instead of the usual comma (','). Asides from that, the algorithms we used - Apriori, FP-Growth, and ECLAT - worked wonders with superb runtime performance. So moving forward, we might recommend PAMI more for big datasets.


The dataset we used were an artificial on-site retail dataset found on kaggle.com and the other being instacart's (online) yearly dataset (2017). When transformed and merged in a transaction-product format (RapidMiner):


    T001 : P001

    T001 : P002

    T002 : P001

    T002 : P003


Combining the Retail and Instacart datasets in this format produced around 36 million rows. When transformed and merged in a sparse dataframe format (PAMI):


    T001 : P001, P002

    T002 : P001, P003


Combining the Retail and Instacart datasets in this format produced around 4 million rows.


In conclusion, we found numerous product baskets that can be used for further analysis, mostly with RapidMiner and the PAMI library.


#### Dataset:
- Instacart Transaction Data  (https://www.kaggle.com/c/instacart-market-basket-analysis_
- Retail Transactions Dataset (https://www.kaggle.com/datasets/prasad22/retail-transactions-dataset)
