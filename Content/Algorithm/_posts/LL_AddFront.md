---
layout: post
title: Linked List Insert In Front of The Head
description: >
This is how to insert node in front of the head.
sitemap: false
group: true
hide_last_modified: true
---

```c++
templae <typename T>
class ListElement {
public:
    ListElement(const T &value) : next(NULL), data(value) {}
    ListElement(const ListElement &rhs) {}
    ~ListElement() {}
    
    ListElement* getNext() const { return nest; }
    const T& getValue() const { return data; }
    void setNext(ListElement *elem) { next = elem; }
    void setValue(const T &value) { data = value; }
    
    ListElement& operator=(const ListElement &rhs) {
        return *this;
    }
    
    // TODO: Need to understand this
    bool insertInFront( ListElement<T> **head, T data) {
        auto *newElem = new ListElement<T>(data);
        
        if (!newElem) return false;
        else {
            newElem->data = data;
            newElem->next = *head;
            *head = newElem;
            return true
        }
    }
private:
    ListElement *next;
    T            data;
}; 
```