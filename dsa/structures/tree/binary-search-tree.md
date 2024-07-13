# Binary Search Tree

It's just binary tree with some logic! Here our tree has some properties like, our root will be greater than everything of it's left and will be less than it's right subtree and so on... So why? What's the point?

> Well, here's the thing, it'll let us find either an elelment exist in our tree or not in O(log\_2 n) time complexity. Pretty kool, right?

## 7.4 Find

Before inserting values, let's actually try to find a value exists in our tree or not. We will iterate through our tree to find the location and previous location of whatever we search for. So if our location is NULL we can just go ahead and use that information while inserting.

```cpp
void find(Node *&root, Node *&location, Node *&previous, int item) {
    location = root;
    previous = NULL;
    if (location == NULL) {
        return;
    }
    while (location != NULL) {
        if (item == location -> data) {
            return;
        } 
        if (item < location -> data) {
            previous = location;
            location = location -> left;
        }
        else {
            previous = location;
            location = location -> right;
        }
    }
}
```

Here we are passing pointer as a reference! Pretty kool, right? We will be using these values later!

## 7.5 Insert

In insertion we will simply use the data of above method. And as always if it's NULL we will try to add that node.

```cpp
void insert(Node *&root, int item) {
    Node *location, *previous;
    find(root, location, previous, item);
    if (location != NULL) return;
    if (previous == NULL)
        root = new Node(item);
    else if (item < previous -> data) 
        previous -> left = new Node(item);
    else 
        previous -> right = new Node(item);
}
```

Suppose we have the location of a node and the location of it's parent node and we are gonna delete that node.

## 7.6 Delete with one child

We will be deleting nodes if any node of our tree has only one child. So we can just go ahead and check either it has a left child or right child and act accordingly.

```cpp
void delete_with_one_child(Node *&root, Node *&location, Node *&parent) {
    Node *child;
    if (location -> left != NULL) 
        child = location -> left;
    else if (location -> right != NULL)
        child = location -> right;
    else 
        child = NULL;
    
    if (parent != NULL) {
        if (location == parent -> left) 
            parent -> left = child;
        else 
            parent -> right = child;
    } else {
        root = child;
    }
}
```

But what if we have two child?

## 7.7 Delete with two child

In this case, things are bit tricky, cause we have to consider which of the successor will take the place of the node that we delete. And actually if we iterate through the right node's left element and so on, we will eventually meet with that guy. Next we can use the above trick to get rid of that alongside joining our new node with parent.

```cpp
void delete_with_two_children(Node *&root, Node *&location, Node *&parent) {
    Node *successor, *parent_successor;
    parent_successor = location;
    successor = location -> right;
    while (successor -> left != NULL) {
        parent_successor = successor;
        successor = successor -> left;
    }
    delete_with_one_child(root, successor, parent_successor);
    if (parent != NULL) {
        if (location == parent -> left) 
            parent -> left = successor;
        else 
            parent -> right = successor;
    } else {
        root = successor;
    }
    successor -> left = location -> left;
    successor -> right = location -> right;
}
```

## 7.8 Deleting an element

As we have seen in the 7.6 and 7.7, we will be needing address of the node that we want to delete. And here in this step we will work around this. We will use 7.4 to find the address of our node and parent and will try to determine either it has one child or two child!

```cpp
void delete_node(Node *&root, int item) {
    Node *location, *parent;
    find(root, location, parent, item);
    if (location == NULL) return;
    if (location -> left != NULL && location -> right != NULL) 
        delete_with_two_children(root, location, parent);
    else 
        delete_with_one_child(root, location, parent);
    delete location;
}
```

## Wrapping up!

After combining all of the above algorithms here's a full executable code,

```cpp
#include <iostream>
#include <stack>
#include <queue>

using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int data) {
        this->data = data;
        left = NULL;
        right = NULL;
    }
};

void find(Node *&root, Node *&location, Node *&previous, int item) {
    location = root;
    previous = NULL;
    if (location == NULL) {
        return;
    }
    while (location != NULL) {
        if (item == location -> data) {
            return;
        } 
        if (item < location -> data) {
            previous = location;
            location = location -> left;
        }
        else {
            previous = location;
            location = location -> right;
        }
    }
}

void insert(Node *&root, int item) {
    Node *location, *previous;
    find(root, location, previous, item);
    if (location != NULL) return;
    if (previous == NULL)
        root = new Node(item);
    else if (item < previous -> data) 
        previous -> left = new Node(item);
    else 
        previous -> right = new Node(item);
}

void delete_with_one_child(Node *&root, Node *&location, Node *&parent) {
    Node *child;
    if (location -> left != NULL) 
        child = location -> left;
    else if (location -> right != NULL)
        child = location -> right;
    else 
        child = NULL;
    
    if (parent != NULL) {
        if (location == parent -> left) 
            parent -> left = child;
        else 
            parent -> right = child;
    } else {
        root = child;
    }
}

void delete_with_two_children(Node *&root, Node *&location, Node *&parent) {
    Node *successor, *parent_successor;
    parent_successor = location;
    successor = location -> right;
    while (successor -> left != NULL) {
        parent_successor = successor;
        successor = successor -> left;
    }
    delete_with_one_child(root, successor, parent_successor);
    if (parent != NULL) {
        if (location == parent -> left) 
            parent -> left = successor;
        else 
            parent -> right = successor;
    } else {
        root = successor;
    }
    successor -> left = location -> left;
    successor -> right = location -> right;
}

void delete_node(Node *&root, int item) {
    Node *location, *parent;
    find(root, location, parent, item);
    if (location == NULL) return;
    if (location -> left != NULL && location -> right != NULL) 
        delete_with_two_children(root, location, parent);
    else 
        delete_with_one_child(root, location, parent);
    delete location;
}

void preorder(Node *root) {
    if (root == NULL) return;
    cout << root -> data << " ";
    preorder(root -> left);
    preorder(root -> right);
}

void inorder(Node *root) {
    if (root == NULL) return;
    inorder(root -> left);
    cout << root -> data << " ";
    inorder(root -> right);
}

void level_order(Node *root) {
    if (root == NULL) return;
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {
        Node *current = q.front();
        q.pop();
        cout << current -> data << " ";
        if (current -> left != NULL) q.push(current -> left);
        if (current -> right != NULL) q.push(current -> right);
    }
}

int main() {
    Node* tree = NULL;
    insert(tree, 60);
    insert(tree, 25);
    insert(tree, 75);
    insert(tree, 15);
    insert(tree, 50);
    insert(tree, 66);
    insert(tree, 33);
    insert(tree, 44);

    cout << "Before Deletion -> \n";
    cout << "Preorder -> \n";
    preorder(tree);
    cout << "\nInorder -> \n";
    inorder(tree);
    cout << "\nLevel Order -> \n";

    delete_node(tree, 25);

    cout << "After Deletion -> \n";
    cout << "Preorder -> \n";
    preorder(tree);
    cout << "\nInorder -> \n";
    inorder(tree);
    cout << "\nLevel Order -> \n";
    level_order(tree);
}
```
