---
permalink: /algorithm/linkedlist
layout: article
title: Linked List
tags: LinkedList
categories: algorithm
article_header:
type: cover
image:
src: 
---
# Linked List

A linked list is a collection of elements, called nodes, 
which consists data and a reference (or link) to the next node in the sequence. 
This structure allows for efficient insertion and deletion of elements.

## Types of Linked Lists

- **Singly Linked List**: 
Each node contains data and a pointer to the next node. 
The last node points to null, indicating the end of the list.

- **Doubly Linked List**: Each node contains data, a pointer to the next node, 
and a pointer to the previous node. This allows traversal in both directions.

- **Circular Linked List**: Similar to singly or doubly linked lists, 
but the last node points back to the first node, forming a circle.

## Advantages

- **Dynamic Size**: Unlike arrays, linked lists are dynamic and can grow or shrink in size.

- **Efficient Insertions/Deletions**: Adding or removing elements from a linked list is generally more efficient than doing so in an array, especially for large datasets.

- **No Memory Wastage**: Linked lists allocate memory as needed, so there's no unused memory like in arrays.

## Disadvantages

- **Memory Usage**: Each node in a linked list requires extra memory for the pointer(s), which can be significant compared to arrays.

- **Sequential Access**: Elements in a linked list must be accessed sequentially, starting from the first node, making random access slow.

- **Complexity**: Implementing and managing a linked list is more complex than an array.

## Basic Operations

- **Traversal**: Going through each node, usually starting from the head, until you reach the end (or a specific condition).
- **Insertion**: Adding a node to the list, either at the beginning, end, or at a specific position.
- **Deletion**: Removing a node from the list, which involves adjusting the pointers of adjacent nodes.
- **Search**: Finding a node in the list with a specific value.

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
        head->insertAtFront(&head, randomCard);
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