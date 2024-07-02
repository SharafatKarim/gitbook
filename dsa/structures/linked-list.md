# Linked List

A linked list is a linear data structure, in which the elements are not stored at contiguous memory locations. The elements in a linked list are linked using pointers.

{% hint style="info" %}
This page will be a bit large. Use the right sidebar to navigate withing the page (desktop mode).
{% endhint %}

## The methodology

There are different ways to implement linked list, like using structures. But I will be using class (OOP) for simplicity. Feel free to use any other websites for exploring different approaches.&#x20;

## 5.1 Traversing

To traverse we will use a simple loop. Check this headless code,

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* link;
    Node(int data) {
        this->data = data;
        link = NULL;
    }
};

class LinkedList {
private:
    Node *start;
public:
    LinkedList() {
        start = NULL;
    }
    void printAll() {
        if (start == NULL) {
            cout << "List is empty!\n";
            return;
        }
        Node *temp = start;
        while (temp != NULL) {
            cout << temp->data << " ";
            temp = temp->link;
        }
        cout << endl;
    }
};

int main() {
    LinkedList list;
    list.printAll();
}
```

Here for storing data we have used an structure. You may use a class as well for this. Here as for the constructor, we are assigning our head/ start node to `NULL`. In the `printAll` method we are using our actual algorithm. As the list is empty, it will print `List is empty`.

## 5.2 Searching

Just like in searching, we will traverse and compare!

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* link;
    Node(int data) {
        this->data = data;
        link = NULL;
    }
};

class LinkedList {
private:
    Node *start;
public:
    LinkedList() {
        start = NULL;
    }
    Node *search(int item) {
        if (start == NULL) {
            cout << "List is empty!\n";
            return NULL;
        }
        Node *temp = start;
        while (temp != NULL) {
            if (temp->data == item) {
                return temp;
            }
            temp = temp->link;
        }
        return NULL;
    }
};

int main() {
    LinkedList list;
    list.search(5);
}
```

Here, it'll also print the list is empty. So we actually need some method to append some data into our list so that we can actually display some output. Right?&#x20;

Let's try altogether in the next example!

## 5.3 Searching a sorted list

The list is sorted? Yeah! So we can just terminate if we find a value higher that we are aiming.

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* link;
    Node(int data) {
        this->data = data;
        link = NULL;
    }
};

class LinkedList {
private:
    Node *start;
public:
    LinkedList() {
        start = NULL;
    }
    void insertFirst(int data) {
        Node *new_node = new Node(data);
        new_node->link = start;
        start = new_node;
    }
    void printAll() {
        if (start == NULL) {
            cout << "List is empty!\n";
            return;
        }
        Node *temp = start;
        while (temp != NULL) {
            cout << temp->data << " ";
            temp = temp->link;
        }
        cout << endl;
    }
    Node *search(int item) {
        if (start == NULL) {
            cout << "List is empty!\n";
            return NULL;
        }
        Node *temp = start;
        while (temp != NULL) {
            if (temp->data == item) {
                return temp;
            }
            temp = temp->link;
        }
        return NULL;
    }
    Node *searchSorted(int item) {
        if (start == NULL) {
            cout << "List is empty!\n";
            return NULL;
        }
        Node *temp = start;
        while (temp != NULL) {
            if (temp->data < item)
                temp = temp->link;
            else if (temp->data == item) 
                return temp;
            else 
                return NULL;
        }
    }
};

int main() {
    LinkedList list;
    list.insertFirst(10);
    list.insertFirst(20);
    list.printAll();
    Node *found_1 = list.search(10);
    if (found_1 != NULL) {
        cout << "Found: " << found_1->data << endl;
    } else {
        cout << "Not found!\n";
    }
    Node *found_2 = list.searchSorted(10);
    if (found_2 != NULL) {
        cout << "Found: " << found_2->data << endl;
    } else {
        cout << "Not found!\n";
    }
}
```

## 5.4 Insert at the beginning

Well, here's two thing to consider, if a list is empty then you are the king, MR. DATA. And otherwise we just have to tweak our start/ header node a bit, right? Check the above code's `insertFirst` method.

## 5.5 Insert at a location

We can actually insert at a location if we know the location, right? Hope you can imagine that,

```cpp
void insertIntoLocation(Node *location, int item) {
        if (location == NULL) {
            insertFirst(item);
            return;
        }
        Node *new_node = new Node(item);
        new_node->link = location->link;
        location->link = new_node;
    }
```

Here we are inserting an item (int) in the location. But the location is a pointer of our node, right? So how can we get this? We have already seen that in 5.2.

Let's assume it's a sorted list. Now what?

## 5.6 Location of Upper Bound - 1

What is upper bound?\
If I have an array with 1 2 2 4 elements, then the upper bound of 3 is position 3 (0 base index). Right?&#x20;

But for our previous 5.4 algorithm to work, we need the location of last occurrence of 2, so our title is, `upper bound - 1`&#x20;

Let's look at the code,\
here we need to trace the history.

```cpp
    Node *findLastSmaller(int item) {
        Node *temp = start;
        Node *prev = NULL;
        while (temp != NULL) {
            if (temp->data < item) {
                prev = temp;
                temp = temp->link;
            } else {
                return prev;
            }
        }
        return prev;
    }
```

## 5.7 Insertion in a sorted list

So if we implement two methods we developed in 5.4 and 5.5, our code will be,

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* link;
    Node(int data) {
        this->data = data;
        link = NULL;
    }
};

class LinkedList {
private:
    Node *start;
public:
    LinkedList() {
        start = NULL;
    }
    void insertFirst(int data) {
        Node *new_node = new Node(data);
        new_node->link = start;
        start = new_node;
    }
    void insertIntoLocation(Node *location, int item) {
        if (location == NULL) {
            insertFirst(item);
            return;
        }
        Node *new_node = new Node(item);
        new_node->link = location->link;
        location->link = new_node;
    }
    Node *findLastSmaller(int item) {
        Node *temp = start;
        Node *prev = NULL;
        while (temp != NULL) {
            if (temp->data < item) {
                prev = temp;
                temp = temp->link;
            } else {
                return prev;
            }
        }
        return prev;
    }
    void printAll() {
        if (start == NULL) {
            cout << "List is empty!\n";
            return;
        }
        Node *temp = start;
        while (temp != NULL) {
            cout << temp->data << " ";
            temp = temp->link;
        }
        cout << endl;
    }
};

int main() {
    LinkedList list;
    list.insertFirst(20);
    list.insertFirst(10);
    list.printAll();
    Node *location = list.findLastSmaller(15);
    list.insertIntoLocation(location, 15);
    list.printAll();
}
```

{% hint style="danger" %}
It has a limitation. While inserting into a sorted list, if the item is greater than all the elements in the list, it will not insert the item at the end of the list. It will insert the item at the beginning of the list. So, we need to modify the code to handle this case.

**Use 25 instead of 15 in the above code, you will get the fact.**

* To solve this issue, we can use an another method like,

```
    void insertIntoSorted(int item) {
        if (start == NULL || start->data >= item) {
            insertFirst(item);
            return;
        }
        Node *location = findLastSmaller(item);
        if (location == NULL) {
            insertLast(item);
            return;
        }
        insertIntoLocation(location, item);
    }
```
{% endhint %}

## 5.8 Delete at a position

For deletion, we will require two locations,&#x20;

* location which value will be erased
* location before the erased value

Why? If we don't have the previous value we need to traverse once more! Or perhaps 2 way linked list? We will check both of 'em. But wait a bit longer for 2 way linked list.

So our basic method is like,

```cpp
    void deleteAtLocation(Node *location, Node *prev_location) {
        if (prev_location == NULL) {
            start = start->link;
        } else {
            prev_location->link = location->link;
        }
        delete location;
    }
```

## 5.9 Location and it's previous location!

We can use an extra variable for preserving previous location, right? Let's check a method,

```cpp
    void findLocationAndPrev(int item, Node *&location, Node *&prev) {
        prev = NULL;
        location = start;
        while (location != NULL) {
            if (location->data == item) {
                return;
            } else {
                prev = location;
                location = location->link;
            }
        }
        location = NULL;
        return;
    }
```

## 5.10 Deletion at the first occurrence

Now combining 5.8 and 5.9 we can achieve this, right? Here's full code,

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* link;
    Node(int data) {
        this->data = data;
        link = NULL;
    }
};

class LinkedList {
private:
    Node *start;
public:
    LinkedList() {
        start = NULL;
    }
    void insertFirst(int data) {
        Node *new_node = new Node(data);
        new_node->link = start;
        start = new_node;
    }
    void insertLast(int data) {
        if (start == NULL) {
            insertFirst(data);
            return;
        }
        Node *temp = start;
        while (temp->link != NULL) {
            temp = temp->link;
        }
        Node *new_node = new Node(data);
        temp->link = new_node;
    }

    void deleteAtLocation(Node *location, Node *prev_location) {
        if (prev_location == NULL) {
            start = start->link;
        } else {
            prev_location->link = location->link;
        }
        delete location;
    }
    void findLocationAndPrev(int item, Node *&location, Node *&prev) {
        prev = NULL;
        location = start;
        while (location != NULL) {
            if (location->data == item) {
                return;
            } else {
                prev = location;
                location = location->link;
            }
        }
        location = NULL;
        return;
    }
    void deleteItem(int item) {
        Node *location, *prev;
        findLocationAndPrev(item, location, prev);
        if (location == NULL) {
            cout << "Item not found!\n";
            return;
        }
        deleteAtLocation(location, prev);
    }

    void printAll() {
        if (start == NULL) {
            cout << "List is empty!\n";
            return;
        }
        Node *temp = start;
        while (temp != NULL) {
            cout << temp->data << " ";
            temp = temp->link;
        }
        cout << endl;
    }
};

int main() {
    LinkedList list;
    list.insertFirst(20);
    list.insertFirst(10);
    list.insertFirst(30);
    list.printAll();

    list.deleteItem(30);
    list.printAll();
}
```

I think, this concludes the basics!\
There are even more things that can be achieved. So good luck! For now let's explore two more perspective,

* header linked list
* 2 way linked list

and finally we can combine them together into,

* 2 way header linked list

***

## Header linked lists

Let's think in this way, in linked lists, when we iterate, what is our sentinel (the point where we stop our loop) value? Well, it's until we actually find NULL. Right?

To make this looping steps a lil bit easy and **NULL free**, we are trying this header linked list! Out of two kinds, grounded and circular, we will be using circular.

## 5.11 Traversing Circular Header List

So just like our 5.1 Traversing, we are traversing, but a bit difference in the looping steps. Compare to understand.

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* link;
    Node(int data) {
        this->data = data;
        link = NULL;
    }
};

class HeaderLinkedList {
private:
    Node *start;
public:
    HeaderLinkedList() {
        start = NULL;
    }
    void insertAtBeginning(int data) {
        Node *new_node = new Node(data);
        if (start == NULL) {
            start = new Node(0);
            start->link = new_node;
            new_node->link = start;
            return;
        }
        new_node->link = start->link;
        start->link = new_node;
    }
    void listAll() {
        if (start == NULL) {
            cout << "List is empty" << endl;
            return;
        }
        Node *temp = start->link;
        while (temp != start) {
            cout << temp->data << " ";
            temp = temp->link;
        }
        cout << endl;
    }
};

int main() {
    HeaderLinkedList list;
    list.insertAtBeginning(10);
    list.insertAtBeginning(20);
    list.insertAtBeginning(50);
    list.insertAtBeginning(5);
    list.listAll();
    return 0;
}
```

## 5.12 Searching in Header list

We will return the first occurance (position). So our code is,

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* link;
    Node(int data) {
        this->data = data;
        link = NULL;
    }
};

class HeaderLinkedList {
private:
    Node *start;
public:
    HeaderLinkedList() {
        start = NULL;
    }
    void insertAtBeginning(int data) {
        Node *new_node = new Node(data);
        if (start == NULL) {
            start = new Node(0);
            start->link = new_node;
            new_node->link = start;
            return;
        }
        new_node->link = start->link;
        start->link = new_node;
    }
    Node *search(int data) {
        if (start == NULL) {
            cout << "List is empty" << endl;
            return NULL;
        }
        Node *temp = start->link;
        while (temp != start) {
            if (temp->data == data) {
                return temp;
            }
            temp = temp->link;
        }
        cout << "Element not found" << endl;
        return NULL;
    }
    void listAll() {
        if (start == NULL) {
            cout << "List is empty" << endl;
            return;
        }
        Node *temp = start->link;
        while (temp != start) {
            cout << temp->data << " ";
            temp = temp->link;
        }
        cout << endl;
    }
};

int main() {
    HeaderLinkedList list;
    list.insertAtBeginning(10);
    list.insertAtBeginning(20);
    list.insertAtBeginning(50);
    list.insertAtBeginning(5);
    list.listAll();
    Node *searched = list.search(10);
    if (searched != NULL) {
        cout << "Element found: " << searched->data << endl;
    }
    return 0;
}
```

## 5.13 Searching location and previous location

Just like 5.9, let's implement this one,

```cpp
    void findLocationAndPrev(int item, Node **prev_location, Node **location) {
        *prev_location = start;
        Node *temp = start->link;
        while (temp != start) {
            if (temp->data == item) {
                *location = temp;
                return;
            }
            *prev_location = temp;
            temp = temp->link;
        }
        *location = NULL;
    }
```

## 5.14 Deletion in Header list

With the support of 5.13 we can finally delete a node just like 5.10, right?

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* link;
    Node(int data) {
        this->data = data;
        link = NULL;
    }
};

class HeaderLinkedList {
private:
    Node *start;
public:
    HeaderLinkedList() {
        start = NULL;
    }
    void insertAtBeginning(int data) {
        Node *new_node = new Node(data);
        if (start == NULL) {
            start = new Node(0);
            start->link = new_node;
            new_node->link = start;
            return;
        }
        new_node->link = start->link;
        start->link = new_node;
    }
    Node *search(int data) {
        if (start == NULL) {
            cout << "List is empty" << endl;
            return NULL;
        }
        Node *temp = start->link;
        while (temp != start) {
            if (temp->data == data) {
                return temp;
            }
            temp = temp->link;
        }
        cout << "Element not found" << endl;
        return NULL;
    }
    
    void findLocationAndPrev(int item, Node **prev_location, Node **location) {
        *prev_location = start;
        Node *temp = start->link;
        while (temp != start) {
            if (temp->data == item) {
                *location = temp;
                return;
            }
            *prev_location = temp;
            temp = temp->link;
        }
        *location = NULL;
    }
    void deleteAtLocation(int item) {
        Node *prev_location, *location;
        findLocationAndPrev(item, &prev_location, &location);
        if (location == NULL) {
            cout << "Element not found" << endl;
            return;
        }
        prev_location->link = location->link;
        delete location;
    }

    void listAll() {
        if (start == NULL) {
            cout << "List is empty" << endl;
            return;
        }
        Node *temp = start->link;
        while (temp != start) {
            cout << temp->data << " ";
            temp = temp->link;
        }
        cout << endl;
    }
};

int main() {
    HeaderLinkedList list;
    list.insertAtBeginning(10);
    list.insertAtBeginning(20);
    list.insertAtBeginning(50);
    list.insertAtBeginning(5);
    list.listAll();
    list.deleteAtLocation(50);
    list.listAll();
    return 0;
}
```

## Two Way Lists

In two way lists, besides storing the next elements location of each node, we will also gather the previous value's location. And it's more fun if we combine, two way lists and headers lists together! Let's rip it,

## 5.15 Deletion in 2-way header

So when we have the location, we can actually link the previous one and the next one altogether to perform teh deletion! So our method is like,

```cpp
    void deleteAtPostion(Node *current) {
        current->prev->next = current->next;
        current->next->prev = current->prev;
        delete current;
        size--;
    }
```

## 5.16 Insertion in 2-way header

Likewise, if we have the positions of two nodes, we can insert easily like,

```cpp
    void insertInBetween(int item, Node *prev, Node *next) {
        Node* newNode = new Node();
        newNode->data = item;
        newNode->next = next;
        newNode->prev = prev;
        prev->next = newNode;
        next->prev = newNode;
        size++;
    }
```

Finally if we wrap 5.15 and 5.16 altogether,&#x20;

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node* prev;
};

class Header2WayLinkedList {
    Node* head;
    Node* tail;
    int size;
public:
    Header2WayLinkedList() {
        head = new Node();
        tail = new Node();
        head->next = tail;
        tail->prev = head;
        size = 0;
    }

    void insertBefore(int data) {
        Node* newNode = new Node();
        newNode->data = data;
        newNode->next = head->next;
        newNode->prev = head;
        head->next->prev = newNode;
        head->next = newNode;
        size++;
    }

    void insertInBetween(int item, Node *prev, Node *next) {
        Node* newNode = new Node();
        newNode->data = item;
        newNode->next = next;
        newNode->prev = prev;
        prev->next = newNode;
        next->prev = newNode;
        size++;
    }

    void getLocationAndPrev(int data, Node* &location, Node* &prev) {
        location = head->next;
        prev = head;
        while (location != tail) {
            if (location->data == data) {
                return;
            }
            prev = location;
            location = location->next;
        }
        location = NULL;
    }        

    void deleteAtPostion(Node *current) {
        current->prev->next = current->next;
        current->next->prev = current->prev;
        delete current;
        size--;
    }

    void remove(int data) {
        Node* current = head->next;
        while (current != tail) {
            if (current->data == data) {
                deleteAtPostion(current);
                return;
            }
            current = current->next;
        }
    }

    void print() {
        Node* current = head->next;
        while (current != tail) {
            cout << current->data << " ";
            current = current->next;
        }
        cout << endl;
    }

    int getSize() {
        return size;
    }
};

int main() {
    Header2WayLinkedList list;
    list.insertBefore(1);
    list.insertBefore(2);
    list.insertBefore(3);
    list.insertBefore(4);
    list.insertBefore(5);
    list.print();

    list.remove(4);
    list.print();
    
    Node *location, *prev;
    list.getLocationAndPrev(3, location, prev);
    if (location == NULL) {
        cout << "Not found" << endl;
    } else {
        list.insertInBetween(4, prev, location);
    }
    list.print();

    return 0;
}
```

{% hint style="info" %}
Here I didn't show the implementation of every single items. So best wishes for you! It's more fun to implement rather than just reading. Good luck!
{% endhint %}

***

## Python implementation

Once I implemented it on python. If you are familliar with python you can check that out for reference from time to time,

{% embed url="https://gist.github.com/SharafatKarim/0e299e5a115293b4116f8d78076920e2" %}
python implementation
{% endembed %}

