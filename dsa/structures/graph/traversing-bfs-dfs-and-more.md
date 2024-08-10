# Traversing - BFS, DFS & More

## Breadth-First Search

In the previous section, remember `printAll()` function?&#x20;

We will be traversing just like that but a different approach. In breadth first, imagine you are a dragon and you are breathing fire in a wood, LOL. So which trees are gonna burn first?&#x20;

> Ovbiously the closer ones, right?

In the breadth first, we are gonna use queue to make a structure from a specific node, add it's adjacent nodes and process the front element one by one. Preety interesting right?

> Instead of writing a brand new code, let' tweak our sweet little code from previous one, we can actually change the core structure and add a new variable named `status`, which will indicate we have visited that or not. In this way,
>
> ```cpp
> class Node {
> public:
>     int data;
>     bool status;
>     Node* next_link; 
>     Node* adjacent;
>     Node* destination;
>
>     Node (int data) {
>         this->data = data;
>         this->next_link = NULL;
>         this->adjacent = NULL;
>         this->destination = NULL;
>         this->status = false;
>     }
>     Node (Node* destination) {
>         this->data = 0;
>         this->next_link = NULL;
>         this->adjacent = NULL;
>         this->destination = destination;
>         this->status = false;
>     }
> };
> ```
>
> Here `true` means we have visited the node. Let's talk about it (code) after DFS.

## Depth-First Search

In DFS, instead of queue, we are going to use stack. That's the difference. I think you can figure out the rest.

And if I complete the code with BFS, our whole code will be,

```cpp
#include <iostream>
#include <queue>
#include <stack>

using namespace std;

class Node {
public:
    int data;
    bool status;
    Node* next_link; 
    Node* adjacent;
    Node* destination;

    Node (int data) {
        this->data = data;
        this->next_link = NULL;
        this->adjacent = NULL;
        this->destination = NULL;
        this->status = false;
    }
    Node (Node* destination) {
        this->data = 0;
        this->next_link = NULL;
        this->adjacent = NULL;
        this->destination = destination;
        this->status = false;
    }
};

class Graph {
    Node* start; 
public:
    Graph() : start(NULL) {}
    
    Node* find(int data) {
        Node* temp = start;
        while (temp != NULL) {
            if (temp->data == data) return temp;
            temp = temp->next_link;
        }
        return NULL;
    }

    void insertNode(int data) {
        Node* new_node = new Node(data);
        if (find(data) != NULL) {
            cout << "Node already exists" << endl;
            return;
        }
        if (start == NULL) {
            start = new_node;
        } else {
            new_node->next_link = start;
            start = new_node;
        }
    }

    void insertEdge(int data1, int data2) {
        Node* node1 = find(data1);
        Node* node2 = find(data2);
        if (node1 == NULL || node2 == NULL) {
            cout << "Node not found" << endl;
            return;
        }
        
        Node* temp = node1->adjacent;
        while (temp != NULL)
        {
            if (temp->destination == node2) {
                cout << "Edge already exists" << endl;
                return;
            }
            temp = temp->next_link;
        }

        Node* new_node = new Node(node2);
        new_node->next_link = node1->adjacent;
        node1->adjacent = new_node;
    }

    void printAll() {
        Node* temp = start;
        while (temp != NULL) {
            cout << temp->data << " -> ";
            Node* temp2 = temp->adjacent;
            while (temp2 != NULL) {
                cout << temp2->destination->data << ", ";
                temp2 = temp2->next_link;
            }
            temp = temp->next_link;
            cout << endl;
        }
    }

    void breadthFirst() {
        queue<Node*> q;
        q.push(start);
        start->status = true;

        while (!q.empty()) {
            Node* temp = q.front();
            cout << temp->data << " ";
            q.pop();
            temp = temp->adjacent;
            while (temp != NULL) {
                if (!temp->destination->status) {
                    q.push(temp->destination);
                    temp->destination->status = true;
                }
                temp = temp->next_link;
            }
        }
        cout << endl;
    }
    
    void depthFirst() {
        stack<Node*> s;
        s.push(start);
        start->status = true;

        while (!s.empty()) {
            Node* temp = s.top();
            cout << temp->data << " ";
            s.pop();
            temp = temp->adjacent;
            while (temp != NULL) {
                if (!temp->destination->status) {
                    s.push(temp->destination);
                    temp->destination->status = true;
                }
                temp = temp->next_link;
            }
        }
        cout << endl;
    }
};

int main() {
    Graph g;
    g.insertNode(1);
    g.insertNode(2);
    g.insertNode(3);

    g.insertEdge(1, 2);
    g.insertEdge(2, 3);
    g.insertEdge(3, 2);
    g.insertEdge(2, 1);

    g.printAll();

    g.breadthFirst();
    // g.depthFirst();

    return 0;
}
```

{% hint style="danger" %}
In the above code, we are directly tweaking the memory of main class Node, and so our visited value will be changed after one BFS or DFS. So we can't use both BFS and DFS at the same time. So what to do?
{% endhint %}

## BFS + DFS

In this case, (above warning) we can actually go ahead and use separate map (STL lib) for both BFS and DFS. Let's check the code,

```cpp
#include <iostream>
#include <queue>
#include <stack>
#include <map>

using namespace std;

class Node {
public:
    int data;
    Node* next_link; 
    Node* adjacent;
    Node* destination;

    Node (int data) {
        this->data = data;
        this->next_link = NULL;
        this->adjacent = NULL;
        this->destination = NULL;
    }
    Node (Node* destination) {
        this->data = 0;
        this->next_link = NULL;
        this->adjacent = NULL;
        this->destination = destination;
    }
};

class Graph {
    Node* start; 
public:
    Graph() : start(NULL) {}
    
    Node* find(int data) {
        Node* temp = start;
        while (temp != NULL) {
            if (temp->data == data) return temp;
            temp = temp->next_link;
        }
        return NULL;
    }

    void insertNode(int data) {
        Node* new_node = new Node(data);
        if (find(data) != NULL) {
            cout << "Node already exists" << endl;
            return;
        }
        if (start == NULL) {
            start = new_node;
        } else {
            new_node->next_link = start;
            start = new_node;
        }
    }

    void insertEdge(int data1, int data2) {
        Node* node1 = find(data1);
        Node* node2 = find(data2);
        if (node1 == NULL || node2 == NULL) {
            cout << "Node not found" << endl;
            return;
        }
        
        Node* temp = node1->adjacent;
        while (temp != NULL)
        {
            if (temp->destination == node2) {
                cout << "Edge already exists" << endl;
                return;
            }
            temp = temp->next_link;
        }

        Node* new_node = new Node(node2);
        new_node->next_link = node1->adjacent;
        node1->adjacent = new_node;
    }

    void printAll() {
        Node* temp = start;
        while (temp != NULL) {
            cout << temp->data << " -> ";
            Node* temp2 = temp->adjacent;
            while (temp2 != NULL) {
                cout << temp2->destination->data << ", ";
                temp2 = temp2->next_link;
            }
            temp = temp->next_link;
            cout << endl;
        }
    }

    void breadthFirst() {
        queue<Node*> q;
        q.push(start);
        map<Node*, bool> visited;
        visited[start] = true;

        while (!q.empty()) {
            Node* temp = q.front();
            cout << temp->data << " ";
            q.pop();
            temp = temp->adjacent;
            while (temp != NULL) {
                if (!visited[temp->destination]) {
                    q.push(temp->destination);
                    visited[temp->destination] = true;
                }
                temp = temp->next_link;
            }
        }
        cout << endl;
    }
    
    void depthFirst() {
        stack<Node*> s;
        s.push(start);
        map<Node*, bool> visited;
        visited[start] = true;

        while (!s.empty()) {
            Node* temp = s.top();
            cout << temp->data << " ";
            s.pop();
            temp = temp->adjacent;
            while (temp != NULL) {
                if (!visited[temp->destination]) {
                    s.push(temp->destination);
                    visited[temp->destination] = true;
                }
                temp = temp->next_link;
            }
        }
        cout << endl;
    }
};

int main() {
    Graph g;
    g.insertNode(1);
    g.insertNode(2);
    g.insertNode(3);

    g.insertEdge(1, 2);
    g.insertEdge(2, 3);
    g.insertEdge(3, 2);
    g.insertEdge(2, 1);

    g.printAll();

    g.breadthFirst();
    g.depthFirst();

    return 0;
}
```

And finally, with the support of STL, we can even write more beautiful codes like this, without worrying about implementing two tables separately. In the above cases, we started from the start point. But we can actually start the DFS and BFS algorithm from any point, and this is the most interesting thing about these two brothers.

```cpp
#include<bits/stdc++.h>

using namespace std;

template<typename T> class Graph {
    map<T, list<T>> adjList;
public:
    Graph() {}
    void addEdge(T u, T v, bool bidir = false) {
        adjList[u].push_back(v);
        if(bidir) adjList[v].push_back(u);
    }

    void print() {
        for(auto i : adjList) {
            cout << i.first << " -> ";
            for(auto entry : i.second) {
                cout << entry << ", ";
            }
            cout << endl;
        }
    }

    void bfs(T src) {
        queue<T> q;
        map<T, bool> visited;
        q.push(src);
        visited[src] = true;
        while(!q.empty()) {
            T node = q.front();
            cout << node << " ";
            q.pop();
            for(auto neighbour : adjList[node]) {
                if(!visited[neighbour]) {
                    q.push(neighbour);
                    visited[neighbour] = true;
                }
            }
        }
    }

    void dfs(T src) {
        stack<T> s;
        map<T, bool> visited;
        s.push(src);
        visited[src] = true;
        while(!s.empty()) {
            T node = s.top();
            cout << node << " ";
            s.pop();
            for(auto neighbour : adjList[node]) {
                if(!visited[neighbour]) {
                    s.push(neighbour);
                    visited[neighbour] = true;
                }
            }
        }
    }
};

int main() {
    Graph<char> g;
    g.addEdge('A', 'F');
    g.addEdge('A', 'C');
    g.addEdge('A', 'B');
    g.addEdge('B', 'G');
    g.addEdge('B', 'C');
    g.addEdge('C', 'F');
    g.addEdge('D', 'C');
    g.addEdge('E', 'D');
    g.addEdge('E', 'C');
    g.addEdge('E', 'J');
    g.addEdge('F', 'D');
    g.addEdge('G', 'C');
    g.addEdge('G', 'E');
    g.addEdge('J', 'D');
    g.addEdge('J', 'K');
    g.addEdge('K', 'E');
    g.addEdge('K', 'G');

    g.print();
    g.bfs('A');

    cout << endl;
    g.dfs('J');

    return 0;
}

```
