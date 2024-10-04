---
permalink: /cpp/VirtualInheritance
layout: article
title: Virtual Inheritance
tags: 
categories: cpp
article_header:
type: cover
image:
src:
---

## Virtual Inheritance시 발생가능한 문제점
![virtual_inheritance](/assets/images/cpp/virtualInheritance/virtualInheritance.png)

```
#include <iostream>

class Animal {
public:
    virtual void speak();
    virtual ~Animal() = default;
private:
    double animalData;
}

class Lion : public Animal {
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


class Tiger : public Animal {
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


int main() {
    Liger liger;
    liger.speak();
    return 0;
}
```

![virtual_inheritance_result](/assets/images/cpp/virtualInheritance/VIresult.png)
**Animal 생성자와 소멸자가 각각 2번씩 쓰임**

## 해결책 ##

