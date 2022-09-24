---
layout: post
title: DC Library
description: >
    This is how to use Data Communication Library.
sitemap: false
group: true
hide_last_modified: true
image: /assets/img/dcgit.png
---
## DC Library Set Up


## DC Library
DC Library, as known as 'Data Communication & Internetworking' Library, is a library created by D'Arcy Smith.
We can use his library as needed in the lab or assignment.


## Git link
If you want to see '.sh' files visit link below:<br/>
[https://github.com/bcitcstdatacomm/dc_scripts](https://github.com/bcitcstdatacomm/dc_scripts)
<br/>


## Set up
**1. Clone repositoy**
```
    git clone https://github.com/bcitcstdatacomm/dc_scripts.git
```

**2. Move directory to 'dc_scripts'**
```
    cd dc_cripts
```

**3. Install 'dc' in *prefer directory***
```
    ./dc-install.sh <prefer directory> gcc g++
```
**Ex) If you want to install dc_library in *work* directory in *Desktop*:**
```
    ./dc-install.sh /Desktop/work gcc g++
```

**4. Edit configuration**
This will let a program search target library<>
> **1) Move to *cd /etc/ld.so.conf.d/***
```
    cd /etc/ld.so.conf.d/
```
> **2) Create configuration file**
```
    nano -w local.conf
```
> **3) Add */usr/local/lib64* and */usr/local/lib* in *local.conf***
```
    /usr/local/lib64
    /usr/local/lib
```

**5. Apply configuration file**
To apply configuration, type:
```
    ldconfig
```

**6. Run cmake**
Tell cmake that we will use *3rdparty* library

> **1) Move to *libconfig* in *dc* directory**
```
    cd /dc/3rdparty/libconfig
```
> **2) Run *cmake --install cmake-build-debug/***
```
    cmake --install cmake-build-debug/
```


## Update when new version released
**1.Go to *dc* and run:**
```
    ./dc-update.sh <prefer directory>
```
**Ex) If you want to update dc_library in *work* directory in *Desktop*:**
```
    ./dc-update.sh /Desktop/work
```

## Now you are ready to GO!