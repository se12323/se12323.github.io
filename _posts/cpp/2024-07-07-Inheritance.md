---
permalink: /cpp/inheritance
layout: article
title: Inheritance
tags: inheritance specifier(access) virtualTable
categories: cpp
article_header:
type: cover
image:
src:
---

## Public
### <span style="color:red">**private 멤버 변수로 접근하는 setPri() => 에러**</span> ###

![specifier_public](/assets/images/cpp/public.png)

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
### <span style="color:red">**private, protected 멤버 변수로 접근하는 setPri() / setPro() => 에러**</span> ###
![specifier_protected](/assets/images/cpp/protected.png)

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


