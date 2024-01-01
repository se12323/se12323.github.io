---
layout: article
permalink: /algorithm.html
title: Linked List
tags: LinkedList
article_header:
type: cover
image:
src: 
---
    
## LinkedList.h 
```c++
#ifndef PIE_LINKEDLIST_H
#define PIE_LINKEDLIST_H

#include <iostream>
#include <cstring>

using namespace std;

template <typename T>
class LinkedList {
public:
    LinkedList() : next(nullptr), data(T()) {}
    LinkedList(const T &value) : next(NULL), data(value) {}
    LinkedList(const LinkedList &cp) : next(NULL), data(cp.data) {
        if (!cp.next)
            next = new LinkedList<T>(*cp.next);
    }

    T& getData() const;
    
    // TODO: Need to understand this
    bool insertAtFront(LinkedList<T> **head, T val);

    // TODO: Need to understand this
    bool insertAtLast(LinkedList<T> **head, T val);

    // TODO: Need to understand this
    bool insertAtIndex(LinkedList<T> **head, T val, int index);
    
    LinkedList<T>* search(LinkedList<T> **head, const T& value);

    bool deleteElement(LinkedList<T> **head, LinkedList<T> *delNode);
    
    void clear(LinkedList<T> **head);
    
    LinkedList& operator=(const LinkedList &rhs) {
        if (this != &rhs) {
            delete next;  // Free existing resources

            data = rhs.data;
            next = (rhs.next ? new LinkedList<T>(*rhs.next) : nullptr);
        }
        return *this;
    }

    class Iterator {
    public:
        Iterator(LinkedList<T>* node) : currentNode(node) {}

        // Dereference operator
        T& operator*() const {
            return currentNode->data;
        }

        // Pre-increment operator
        Iterator& operator++() {
            currentNode = currentNode->next;
            return *this;
        }

        // Equality comparison
        bool operator!=(const Iterator& other) const {
            return currentNode != other.currentNode;
        }
    private:
        LinkedList<T>* currentNode;
    };

    // Methods to get iterators
    Iterator begin() { return Iterator(this); }
    Iterator end() { return Iterator(nullptr); }

private:
    LinkedList  *next;
    T            data;
};

#endif //PIE_LINKEDLIST_H
```

## LinkedList.cpp
```c++
#include "LinkedList.h"


template<typename T>
T &LinkedList<T>::getData() const {
    return data;
}


template<typename T>
bool LinkedList<T>::insertAtLast(LinkedList<T> **head, T val) {
    auto *newNode = new LinkedList<T>(val);

    if (!newNode) return false;

    if (*head == NULL) {
        newNode->next = *head;
        *head = newNode;
        return true;
    }
    else {
        LinkedList<T> *temp = *head;
        while (temp->next) {
            temp = temp->next;
        }
        temp->next = newNode;
        return true;
    }
}


template<typename T>
bool LinkedList<T>::insertAtFront(LinkedList<T> **head, T val) {
    auto *newNode = new LinkedList<T>(val);
    if (newNode == nullptr) return false;
    else {
        newNode->data = val;
        newNode->next = *head;
        *head = newNode;
        return true;
    }
}


template<typename T>
bool LinkedList<T>::insertAtIndex(LinkedList<T> **head, T val, int index) {
    LinkedList<T> *current = *head;
    if (*head == nullptr)   return false;
    if (index <= 0)         return false;

    auto *newNode = new LinkedList<T>(val);
    if (!newNode)           return false;

    if (index == 1) {
        *head = newNode;
        newNode->next = current;
        return true;
    }
    else {
        for (int i = 1; i < index; ++i) {
            // If index is greater than the number of nodes in the list
            if (current->next == nullptr) {
                delete newNode;
                return false;
            }
            current = current->next;
        }

        current->next = newNode;
        newNode->next = current->next;
        return true;
    }
}


template<typename T>
LinkedList<T>* LinkedList<T>::search(LinkedList<T> **head, const T& value) {
    LinkedList<T> *current = *head;

    while (current != nullptr) {
        if (current->data == value) {
            return current; // Value found
        }
        current = current->next;
    }

    return nullptr; // Value not found
}


template<typename T>
bool LinkedList<T>::deleteElement(LinkedList<T> **head, LinkedList<T> *delNode) {
    if (*head == nullptr || delNode == nullptr) {
        return false;
    }

    if (*head == delNode) {
        LinkedList<T> *temp = *head;
        *head = (*head)->next;
        delete temp;
        return true;
    }

    LinkedList<T> *current = *head;
    LinkedList<T> *prev = nullptr;
    while (current != nullptr && current != delNode) {
        prev = current;
        current = current->next;
    }

    // Node not found
    if (current == nullptr) {
        return false;
    }

    // Node found
    prev->next = current->next;
    delete current;
    return true;
}


template<typename T>
void LinkedList<T>::clear(LinkedList<T> **head) {
    if (*head == nullptr) return;
    LinkedList<T> *delNode = *head;
    while (delNode) {
        // Todo: if Node data used dynamic memory, need to delete as well
        LinkedList<T> *after = delNode->next;
        delete delNode;
        delNode = after;
    }
    *head = nullptr;
}
```

## main.cpp
```c++
#include "LinkedList.h"
#include "LinkedList.cpp"
#include <ctime>


typedef struct cards{
    char* shape;
    int num;
} card;

const char* shapes[] = {"Heart", "Diamond", "Clover", "Spade"};

card generateRandomCard() {
    card newCard;
    newCard.shape = (char*)shapes[std::rand() % 4]; // Randomly select a shape
    newCard.num = std::rand() % 13 + 1; // Randomly select a number between 1 and 13
    return newCard;
}

int main() {
    std::srand(std::time(nullptr));
    LinkedList<card>* head = nullptr;

    for (int i = 0; i < 5; i++) {
        card randomCard = generateRandomCard();
        // TODO: This is for original LinkedList
        head->insertToFront(&head, randomCard);
    }

//    for (auto it = head->begin(); it != head->end(); ++it) {
//        card c = *it;
//        std::cout << "Card: " << c.shape << " " << c.num << std::endl;
//    }

    for (auto c : *head) {
        std::cout << "Card: " << c.shape << " " << c.num << std::endl;
    }
    
    head->clear(&head);
}
```