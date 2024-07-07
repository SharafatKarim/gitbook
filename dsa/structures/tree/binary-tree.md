# Binary Tree

Binary tree is more like a tree with at most two branches per each node. So you can easily implement it with linked list. In the programming, you can just go ahead and make your class with `left` and `right` pointer variables or perhaps a structure in c++?

## Implementation

Here's an example structure,

```cpp
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
```

To insert elements, we can implement a function which will simply return the instance of the above structure.

```cpp
Node *insert(Node *root, int data) {
    Node *newNode = new Node(data);
    if (root == NULL) {
        root = newNode;
        return root;
    }
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {
        Node *temp = q.front();
        q.pop();
        if (temp->left == NULL) {
            temp->left = newNode;
            return root;
        } else {
            q.push(temp->left);
        }
        if (temp->right == NULL) {
            temp->right = newNode;
            return root;
        } else {
            q.push(temp->right);
        }
    }
    return root;
}
```

## 7.1 Preorder Traversal

While traversing, each node has left and right elements, and let's not forget the root. So if we print or process root at first and then left and right node sequentially, that will be our preorder. Things can be a bit tricky if our tree is long. So, we can actually go ahead and use stack for implementing so,

```cpp
void preOrderTraversal_Iterative(Node *root) {
    stack<Node*> s;
    s.push(root);
    while (!s.empty()) {
        Node *temp = s.top();
        s.pop();
        cout << temp->data << " ";
        if (temp->right != NULL) {
            s.push(temp->right);
        }
        if (temp->left != NULL) {
            s.push(temp->left);
        }
    }
}
```

Want even more crazier method? Check this code and laugh later!

```cpp
void preOrderTraversal_Recursion(Node *root) {
    if (root == NULL) {
        return;
    }
    cout << root->data << " ";
    preOrderTraversal_Recursion(root->left);
    preOrderTraversal_Recursion(root->right);
}
```

Preety kool, right?

## 7.2 Inorder Traversal

In inorder traversal just like preorder we will visit our fellow members but the difference is that we will visit our root after traversing the lefter one!

```cpp
void inOrderTraversal_Iterative(Node *root) {
    stack<Node*> s;
    Node *curr = root;
    while (curr != NULL || !s.empty()) {
        while (curr != NULL) {
            s.push(curr);
            curr = curr->left;
        }
        curr = s.top();
        s.pop();
        cout << curr->data << " ";
        curr = curr->right;
    }
}
```

And for the recursion, just like before, but print after first call,

```cpp
void inOrderTraversal_Recursion(Node *root) {
    if (root == NULL) {
        return;
    }
    inOrderTraversal_Recursion(root->left);
    cout << root->data << " ";
    inOrderTraversal_Recursion(root->right);
}
```

## 7.3 Postorder Traversal

Finally in postorder we will visit our root after we visit it's left and right childrens. Interesting right?

Let's implement in this way,

```cpp
void postOrderTraversal_Iterative(Node *root) {
    stack<pair<Node*, bool>> s;
    s.push(make_pair(root, true));
    while (!s.empty()) {
        Node *temp = s.top().first;
        bool right_sided = s.top().second;
        if (right_sided) {
            s.pop();
            while(temp != NULL) {
                s.push(make_pair(temp, false));
                if (temp->right != NULL) {
                    s.push(make_pair(temp->right, true));
                }
                temp = temp->left;
            } 
        }
        right_sided = s.top().second;
        if (!right_sided) {
            cout << s.top().first->data << " ";
            s.pop();
        }
    }
}
```

Please check the text book for understanding the above code. Here we are using `pair` for storing two characteristics per each stack element. But feel free to use any other method.

Here's an another interesting method, where we can just go ahead and use 2 different stack for storing and organizing our elements,

```cpp
void postOrderTraversal_Iterative_2(Node *root) {
    stack<Node*> s1;
    stack<Node*> s2;
    s1.push(root);
    while (!s1.empty()) {
        Node *temp = s1.top();
        s1.pop();
        s2.push(temp);
        if (temp->left != NULL) {
            s1.push(temp->left);
        }
        if (temp->right != NULL) {
            s1.push(temp->right);
        }
    }
    while (!s2.empty()) {
        cout << s2.top()->data << " ";
        s2.pop();
    }
}
```

And finally le'ts not forget recursion, my most favorite (cause it's easy),

```cpp
void postOrderTraversal_Recursion(Node *root) {
    if (root == NULL) {
        return;
    }
    postOrderTraversal_Recursion(root->left);
    postOrderTraversal_Recursion(root->right);
    cout << root->data << " ";
}
```

And yeah, feel free to try building in your way!

## Wrapping up!

Before wrapping lem'me share an another interesting traversing method, that may come handy later, level order traversing,

```cpp
void levelOrderTraversal(Node *root) {
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {
        Node *temp = q.front();
        q.pop();
        cout << temp->data << " ";
        if (temp->left != NULL) {
            q.push(temp->left);
        }
        if (temp->right != NULL) {
            q.push(temp->right);
        }
    }
}
```

It's like how we actually build our tree. Kool, right?

Here's the full code, you can go ahead and execute,

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

Node *insert(Node *root, int data) {
    Node *newNode = new Node(data);
    if (root == NULL) {
        root = newNode;
        return root;
    }
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {
        Node *temp = q.front();
        q.pop();
        if (temp->left == NULL) {
            temp->left = newNode;
            return root;
        } else {
            q.push(temp->left);
        }
        if (temp->right == NULL) {
            temp->right = newNode;
            return root;
        } else {
            q.push(temp->right);
        }
    }
    return root;
}
    
void preOrderTraversal_Recursion(Node *root) {
    if (root == NULL) {
        return;
    }
    cout << root->data << " ";
    preOrderTraversal_Recursion(root->left);
    preOrderTraversal_Recursion(root->right);
}

void preOrderTraversal_Iterative(Node *root) {
    stack<Node*> s;
    s.push(root);
    while (!s.empty()) {
        Node *temp = s.top();
        s.pop();
        cout << temp->data << " ";
        if (temp->right != NULL) {
            s.push(temp->right);
        }
        if (temp->left != NULL) {
            s.push(temp->left);
        }
    }
}

void inOrderTraversal_Recursion(Node *root) {
    if (root == NULL) {
        return;
    }
    inOrderTraversal_Recursion(root->left);
    cout << root->data << " ";
    inOrderTraversal_Recursion(root->right);
}

void inOrderTraversal_Iterative(Node *root) {
    stack<Node*> s;
    Node *curr = root;
    while (curr != NULL || !s.empty()) {
        while (curr != NULL) {
            s.push(curr);
            curr = curr->left;
        }
        curr = s.top();
        s.pop();
        cout << curr->data << " ";
        curr = curr->right;
    }
}

void postOrderTraversal_Recursion(Node *root) {
    if (root == NULL) {
        return;
    }
    postOrderTraversal_Recursion(root->left);
    postOrderTraversal_Recursion(root->right);
    cout << root->data << " ";
}

void postOrderTraversal_Iterative(Node *root) {
    stack<Node*> s1;
    stack<Node*> s2;
    s1.push(root);
    while (!s1.empty()) {
        Node *temp = s1.top();
        s1.pop();
        s2.push(temp);
        if (temp->left != NULL) {
            s1.push(temp->left);
        }
        if (temp->right != NULL) {
            s1.push(temp->right);
        }
    }
    while (!s2.empty()) {
        cout << s2.top()->data << " ";
        s2.pop();
    }
}

void levelOrderTraversal(Node *root) {
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {
        Node *temp = q.front();
        q.pop();
        cout << temp->data << " ";
        if (temp->left != NULL) {
            q.push(temp->left);
        }
        if (temp->right != NULL) {
            q.push(temp->right);
        }
    }
}

int main() {
    Node *tree = NULL;
    tree = insert(tree, 10);
    tree = insert(tree, 20);
    tree = insert(tree, 30);
    tree = insert(tree, 40);
    tree = insert(tree, 50);
    tree = insert(tree, 60);
    tree = insert(tree, 70);
    tree = insert(tree, 80);
    tree = insert(tree, 90);
    tree = insert(tree, 100);

    cout << "Preorder Traversal (Recursion): ";
    preOrderTraversal_Recursion(tree);
    cout << endl;
    cout << "Preorder Traversal (Iterative): ";
    preOrderTraversal_Iterative(tree);
    cout << endl;
    cout << "Inorder Traversal (Recursion): ";
    inOrderTraversal_Recursion(tree);
    cout << endl;
    cout << "Inorder Traversal (Iterative): ";
    inOrderTraversal_Iterative(tree);
    cout << endl;
    cout << "Postorder Traversal (Recursion): ";
    postOrderTraversal_Recursion(tree);
    cout << endl;
    cout << "Postorder Traversal (Iterative): ";
    postOrderTraversal_Iterative(tree);
    cout << endl;

    cout << "Level Order Traversal: ";
    levelOrderTraversal(tree);
    cout << endl;

    return 0;
}
```
