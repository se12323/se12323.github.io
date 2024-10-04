---
permalink: /cpp/MultipleInheritance
layout: article
title: Multiple Inheritance
tags: 
categories: cpp
article_header:
type: cover
image:
src:
---
![multiple_inheritance](/assets/images/cpp/multipleInheritance/multipleInheritance.png)

```
#include <iostream>

class Lion {
public:
    Lion() {
        std::cout << "Lion Consturctor" << std::endl;
    }

    virtual void speak() {
        std::cout << "Lion!" << std::endl;
    }

    virtual ~Lion() {
        std::cout << "Lion Desturctor" << std::endl;
    }

private: 
    double lionData;
};


class Tiger {
public:
    Tiger() {
        std::cout << "Tiger Consturctor" << std::endl;
    }

    virtual void speak() {
        std::cout << "Tiger!" << std::endl;
    }

    virtual ~Tiger() {
        std::cout << "Tiger Desturctor" << std::endl;
    }

private:
    double tigerData;
};


class Liger : public Tiger, public Lion {
public:
    Liger() {
        std::cout << "Liger Consturctor" << std::endl;
    }

    virtual void speak() override {
        std::cout << "Liger!" << std::endl;
    }

    virtual ~Liger() {
        std::cout << "Liger Desturctor" << std::endl;
    }

private:
    double ligerData;
};

```

## Size of Derived class 
![multiple_inheritance](/assets/images/cpp/multipleInheritance/ligerSize.png)


## Virtual Table 작동 방식
### polyLion ###
```
int main() {
    Tiger *polyLion = new Liger();
    polyLion->speak(); // virtual table 포인터는 라이거를 가리킴
    delete polyLion;
    return 0;
}
```
![polyLion](/assets/images/cpp/multipleInheritance/lion.png)

### polyTiger ###
```
int main() {
    Tiger *polyTiger = new Liger();
    polyTiger->speak(); // virtual table 포인터는 라이거를 가리킴
    delete polyTiger;
    return 0;
}
```
![polyLion](/assets/images/cpp/multipleInheritance/tiger.png)

### ligerPtr ###
```
int main() {
    Liger *ligerPtr = new Liger();
    ligerPtr->speak(); // Lion, Tiger의 virtual table 모두 라이거를 가리킴
    delete ligerPtr;
    return 0;
}
```
![ligerPtr](/assets/images/cpp/multipleInheritance/liger.png)
