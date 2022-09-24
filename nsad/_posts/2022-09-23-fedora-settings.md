---
layout: post
title: Fedora Settings
description: >
  I've put the necessary settings in Fedora here to start our journey. If you need any corrections, feel free to comment.
sitemap: false
group: true
hide_last_modified: true
image: /assets/img/fedora.jpeg
---

## Fedora Linux
Fedora Linux is a Linux distribution developed by the Fedora Project and is the upstream source for Red Hat Enterprise Linux.

Since the release of Fedora 35, six different editions are made available tailored to personal computer, server, cloud computing, container and Internet of Things installations. A new version of Fedora Linux is released every six months.


## Update Yum database

Update yum database with dnf using the following command.
```
  sudo dnf makecache --refresh
```

The output should look something like this:<br/> 
(or more; depend on your packages that were installed for additional)
```
  Fedora 36 - x86_64                               34 kB/s |  22 kB     00:00    
  Fedora 36 openh264 (From Cisco) - x86_64        2.7 kB/s | 989  B     00:00    
  Fedora Modular 36 - x86_64                       51 kB/s |  22 kB     00:00    
  Fedora 36 - x86_64 - Updates                     45 kB/s |  19 kB     00:00    
  Fedora 36 - x86_64 - Updates                    614 kB/s | 2.9 MB     00:04    
  Fedora Modular 36 - x86_64 - Updates             41 kB/s |  19 kB     00:00    
  Metadata cache created.
```

## Instruction

#### 1) ssh
```
  sudo dnf install ssh
```

#### 2) git
```
  sudo dnf install git
```

#### 3) curl
```
  sudo dnf install curl
```

#### 4) gcc
```
  sudo dnf install gcc
```

#### 5) g++
```
  sudo dnf install g++
```

#### 6) clang
```
  sudo dnf install clang
```

#### 7) make
```
  sudo dnf install make
```

#### 8) lldb
```
  sudo dnf install lldb
```

#### 9) clang-tools-extra
```
  sudo dnf install clang-tools-extra
```

#### 10) clang-format
```
  sudo dnf install clang-format
```

#### 11) cmake
```
  sudo pip install cmake
```

#### 12) graphviz
```
  sudo dnf install graphviz
```

#### 13) libgdbm-compat-dev
```
  sudo dnf install libgdbm-compat-dev
```

#### 14) libgdbm-dev
```
  sudo dnf install libgdbm-dev
```

#### 15) doxygen
```
  sudo dnf -y install doxygen
```

#### 16) libasan
```
  sudo dnf -y install libasan
```

#### 17) libubsan
```
  sudo dnf -y install libubsan
```