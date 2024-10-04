---
permalink: /cpp/inheritance
layout: article
title: Inheritance
tags: inheritance specifier(access) virtualTable abstract pureVirtual interface
categories: cpp
article_header:
type: cover
image:
src:
---
## Base Class Destructor
**상속을 사용하는데 있어서 Base class의 Destructor는 <span style="color:red">무조건 virtual public / protected</span> 로 사용**
```
#include  <iostream>

class Animal {
public:
    Animal() {
        std::cout << "Animal constructor" << std::endl;
    }
    
    virtual ~Animal() {  // VIRTUAL PUBLIC
        std::cout << "Animal Destructor" << std::endl;
    }
};


class Cat : public Animal {
public:
    Cat() {
        std::cout << "Cat constructor" << std::endl;
    }

    ~Cat() {
        std::cout << "Cat Destructor" << std::endl;
    }
};

int main() {
    Animal* polyCat = new Cat();
    delete polyCat;
    // 소멸자에 virtual이 없었다면,
    // Animal Constructor
    // Cat Constructor
    // Animal Desstructor
    // 만 출력이됨
}
```

## Public
**<span style="color:red">private 멤버 변수로 접근하는 setPri() => 에러</span>**
![specifier_public](/assets/images/cpp/Inheritance/public.png)

```
class Base {
public: // 자식 클래스에서 Public 으로 봄
    void setPri(int n) {
        pri = n;
    }

    void setPro(int n) {
        pro = n;
    }

protected:
    int pro

private: 
    int pri
};


class Derived : public Base {
public:
    void test() {
        Base::pro = 100;
        Base::pri = 0;  // Compile 에러남
    }
}
```


## Protected
**<span style="color:red">private, protected 멤버 변수로 접근하는 setPri() / setPro() => 에러</span>**
![specifier_protected](/assets/images/cpp/Inheritance/protected.png)

```
class Base {
public: // 자식 클래스에서 Protected 으로 봄
    void setPri(int n) {
        pri = n;
    }

    void setPro(int n) {
        pro = n;
    }

protected:
    int pro

private: 
    int pri
};


class Derived : public Base {
public:
    void test() {
        Base::pro = 100; // Compile 에러남
        Base::pri = 0;   // Compile 에러남
    }
}
```

## Virtual function 사용 전 Class 사이즈
![before_virtual_func](/assets/images/cpp/Inheritance/bvf.png)

```
#include  <iostream>

class Animal {
public:
    void speak() {
        std::cout << "Animal" << std::endl;
    }
    // virtual ~Animal() = default

private:
    double height;
};


class Cat : public Animal {
public:
    speak override {
        std::cout << "Meow" << std::endl;
    }

private:
    double weight;
};

```

## Virtual function 사용 후 Class 사이즈
![after_virtual_func](/assets/images/cpp/Inheritance/avf.png)

```
#include  <iostream>

class Animal {
public:
    virtual void speak() {
        std::cout << "Animal" << std::endl;
    }
    // virtual ~Animal() = default

private:
    double height;
};


class Cat : public Animal {
public:
    void speak override {
        std::cout << "Meow" << std::endl;
    }

private:
    double weight;
};

```

## Virtual 사용 Stack / Heap 분석
![stack_heap_object](/assets/images/cpp/Inheritance/stack_heap.png)
```
int main() {
    Animal *polyAnimal = new Cat();
    // Animal *polyAnimal = new Animal(); // 힙상에 있는 오브젝트가 Animal로 바뀜
    polyAnimal->speak();
    delete polyAnimal
}
```

## Abstract Class
- **<span style="color:red">Pure Virtual function = 0</span> 하나라도 가지고 있는 Class**
- **오브젝트 생성이 <span style="color:red">불가능</span>**


## Interface Class (for 유지 보수)
- **Interface class를 만들때는 멤버 변수를 사용하지 않는다**
- **모든 함수를 pure virtual function = 0 으로 만들어줌**
