# OsmocomBB as research and measurement platform
## Network load measurement
![](https://raw.githubusercontent.com/K1two2/osmocom/master/img/netload.png)
#### measurement.patch

This patch allow you to make load measurements of any cell network. Using modified ccch_scan application you will get statistics in CSV format.

Measurement objects:
+ **Paging Requests** count
  + **Paging Request Type 1**
  + **Paging Request Type 2**
  + **Paging Request Type 3**
+ **Immediate Assignments** count
  + **Normal** or **Extended**
  + **Hopping** or **Non Hopping** channels
+ **Paged subscribers** count
  + Paged by **TMSI**
  + Paged by **IMSI**

###### How to install
    git clone git://git.osmocom.org/osmocom-bb.git
    cd osmocom-bb
    # Copy measurement.patch here
    patch -p1 < measurement.patch
    cd src
    # Make sure that you have ARM Toolchain installed (see project wiki)
    make

###### How to use
    # In first terminal
    cd osmocom-bb/src/
    # This command may differ in you case depending on your phone model
    host/osmocon/osmocon -m c123xor -p /dev/ttyUSB0 target/firmware/board/compal_e88/layer1.compalram.bin
    
    # In second terminal
    cd osmocom-bb/src/host/layer23/src/misc
    ./ccch_scan -a <ARFCN> -l <LOGFILE> -t <OBSERVATION_TIME> -p <LOGGING_INTERVAL>
    
###### Logfile example
    timestamp;pr_total;pd_total;ia_total;pr1;pr2;pr3;ia_default;ia_extended;ia_hoppig;ia_non_hopping;pd_imsi;pd_tmsi
    1446821926;305;165;1;295;8;2;1;0;0;1;20;145
    1446821936;372;234;2;348;19;5;2;0;0;2;28;206
    1446821946;372;220;0;355;14;3;0;0;0;0;28;192
