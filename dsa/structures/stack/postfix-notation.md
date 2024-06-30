# Postfix notation

## Intro

Imagine a pc solving an infix or prefix notation. A bit weird, right?&#x20;

To solve this issue, we actually use postfix! It's actually kinda easy to solve postfix, but a bit tough to convert from infix to postfix.

First comes the way to solve a postfix notation,

## 6.3 Postfix Equation solve

```cpp
#include<iostream>
#include <stack>
#include <queue>

using namespace std;

string solvePostfix_1(queue<string> input_list) {
    stack<string> st;
    while (!input_list.empty()) {
        string token = input_list.front();
        input_list.pop();
        if (token == "+" || token == "-" || token == "*" || token == "/") {
            string operand2 = st.top();
            st.pop();
            string operand1 = st.top();
            st.pop();
            if (token == "+") {
                st.push(to_string(stoi(operand1) + stoi(operand2)));
            } else if (token == "-") {
                st.push(to_string(stoi(operand1) - stoi(operand2)));
            } else if (token == "*") {
                st.push(to_string(stoi(operand1) * stoi(operand2)));
            } else if (token == "/") {
                st.push(to_string(stoi(operand1) / stoi(operand2)));
            }
        } else {
            st.push(token);
        }
    }
    return st.top();
}

string solvePostfix_2(queue<string> input_list) {
    stack<string> st;
    int first_operator, second_operator;
    while (!input_list.empty()){
        switch (input_list.front().at(0))
        {
        case '+':
            second_operator = stoi(st.top()); st.pop();
            first_operator = stoi(st.top()); st.pop();
            st.push(to_string( first_operator + second_operator ));
            break;
        
        case '-':
            second_operator = stoi(st.top()); st.pop();
            first_operator = stoi(st.top()); st.pop();
            st.push(to_string( first_operator - second_operator ));
            break;
        
        case '*':
            second_operator = stoi(st.top()); st.pop();
            first_operator = stoi(st.top()); st.pop();
            st.push(to_string( first_operator * second_operator ));
            break;
        
        case '/':
            second_operator = stoi(st.top()); st.pop();
            first_operator = stoi(st.top()); st.pop();
            st.push(to_string( first_operator / second_operator ));
            break;
        
        default:
            st.push(input_list.front());
            break;
        }
        input_list.pop();
    }
    return st.top();
}

int main() {
    queue<string> input_list({"5","6","2","+","*","12","4","/","-"});
    cout << solvePostfix_1(input_list) << "\n";
    cout << solvePostfix_2(input_list) << "\n";
    return 0;
}    
```

Here `solvePostfix_1` and `solvePostfix_2` are 2 different approach. Nothing to worry. But why queue? Actually you can just go ahead and use string or whatever you like, but think of,&#x20;

**`512+`**, is it `5+12` or `51+2` ?

That's the reason of my using queue. And here I just solved an equation but how about the converstion from infix to postfix?

## 6.4 Postfix conversation

```cpp
#include<iostream>
#include <stack>
#include <queue>

using namespace std;

int precendenceReturn(string str) {
    switch (str.at(0))
    {
    case '+':
        return 1;
        break;
    case '-':
        return 1;
        break;
    case '*':
        return 2;
        break;
    case '/':
        return 2;
        break;
    case '^':
        return 3;
        break;
    default:
        return 0;
        break;
    }
}

string toPostfix(queue<string> input_list) {
    stack<string> st;
    string postfix = "";
    input_list.push(")");
    while (!input_list.empty()) {
        string token = input_list.front();
        input_list.pop();
        if (token == "+" || token == "-" || token == "*" || token == "/" || token == "^") {
            if (!st.empty() && precendenceReturn(st.top()) > precendenceReturn(token)) {
                postfix += st.top();
                st.pop();
            }
            st.push(token);
        } else if (token == "(") {
            st.push(token);
        } else if (token == ")") {
            while (!st.empty()) {
                if (st.top() == "(") {st.pop(); break;}
                postfix += st.top();
                st.pop();
            }
        } else {
            postfix += token;
        }
    }
    return postfix;
}

int main() {
    // Well we can take input from the user in this way [OPTIONAL]
    // -------------------------------------------------------------------
    // string input;
    // // cin >> input; // If there is space in input this line won't gonna work
    // getline(cin, input); // Taking whole line as input
    // queue<string> input_list;
    // string temp_string = "";
    // for (int i = 0; i < input.size(); i++) {
    //     if (input[i] == ' ') continue; // Avoiding spaces
    //     if (isdigit(input[i])) temp_string += input[i];
    //     else { 
    //         if(!temp_string.empty()) input_list.push(temp_string); 
    //         temp_string = ""; 
    //         input_list.push(string(1, input[i]));
    //     }
    // }
    // if(!temp_string.empty()) input_list.push(temp_string); 

    // The following lines are to print the queue (input list)
    // But the queue will be empty later on [WARNING]
    // while (input_list.size()) {
    //     cout << input_list.front() << " ";
    //     input_list.pop();
    // }

    // Or, We can Directly initialize our queue in this way [OPTIONAL]
    // -------------------------------------------------------------------
    queue<string> input_list({"A","+","(","B","*","C","-","(","D","/","E","^","F",")","*","G",")","*","H"});
    // queue<string> input_list({"A","+","B"}); // Simpler one!
    
    // Finally we can call our function toPostfix
    // -------------------------------------------------------------------
    cout << toPostfix(input_list) << "\n";
    
    return 0;
}
```

Here a lot of lines are commented out, right? Well, it's so that you can just take the input from the user.

## The full version

So how about combining these 2, so that we can take input from the user in anyway he likes, and then solving it? Here's the combined edition (and you can understand why we used queue),

```cpp
#include<iostream>
#include <stack>
#include <queue>
#include <math.h>

using namespace std;

string solvePostfix(queue<string> input_list) {
    stack<string> st;
    while (!input_list.empty()) {
        string token = input_list.front();
        input_list.pop();
        if (token == "+" || token == "-" || token == "*" || token == "/" || token == "^") {
            string operand2 = st.top();
            st.pop();
            string operand1 = st.top();
            st.pop();
            if (token == "+") {
                st.push(to_string(stoi(operand1) + stoi(operand2)));
            } else if (token == "-") {
                st.push(to_string(stoi(operand1) - stoi(operand2)));
            } else if (token == "*") {
                st.push(to_string(stoi(operand1) * stoi(operand2)));
            } else if (token == "/") {
                st.push(to_string(stoi(operand1) / stoi(operand2)));
            } else if (token == "^") {
                st.push(to_string(pow(stoi(operand1), stoi(operand2))));
            }
        } else {
            st.push(token);
        }
    }
    return st.top();
}

int precendenceReturn(string str) {
    switch (str.at(0))
    {
    case '+':
        return 1;
        break;
    case '-':
        return 1;
        break;
    case '*':
        return 2;
        break;
    case '/':
        return 2;
        break;
    case '^':
        return 3;
        break;
    default:
        return 0;
        break;
    }
}

queue<string> toPostfix(queue<string> input_list) {
    stack<string> st;
    queue<string> postfix;
    input_list.push(")");
    while (!input_list.empty()) {
        string token = input_list.front();
        input_list.pop();
        if (token == "+" || token == "-" || token == "*" || token == "/" || token == "^") {
            if (!st.empty() && precendenceReturn(st.top()) > precendenceReturn(token)) {
                postfix.push(st.top());
                st.pop();
            }
            st.push(token);
        } else if (token == "(") {
            st.push(token);
        } else if (token == ")") {
            while (!st.empty()) {
                if (st.top() == "(") {st.pop(); break;}
                postfix.push(st.top());
                st.pop();
            }
        } else {
            postfix.push(token);
        }
    }
    return postfix;
}

// // Debugging purpose
// void printQueue(queue<string> input_list) {
//     while (!input_list.empty()) {
//         cout << " <-" << input_list.front() << "-> ";
//         // cout << input_list.front();
//         input_list.pop();
//     }
// }

int main() {
    // Well we can take input from the user in this way [OPTIONAL]
    // -------------------------------------------------------------------
    string input;
    // cin >> input; // If there is space in input this line won't gonna work
    getline(cin, input); // Taking whole line as input
    queue<string> input_list;
    string temp_string = "";
    for (int i = 0; i < input.size(); i++) {
        if (input[i] == ' ') continue; // Avoiding spaces
        if (isdigit(input[i])) temp_string += input[i];
        else { 
            if(!temp_string.empty()) input_list.push(temp_string); 
            temp_string = ""; 
            input_list.push(string(1, input[i]));
        }
    }
    if(!temp_string.empty()) input_list.push(temp_string); 

    // The following lines are to print the queue (input list)
    // But the queue will be empty later on [WARNING]
    // while (input_list.size()) {
    //     cout << input_list.front() << " ";
    //     input_list.pop();
    // }

    // Or, We can Directly initialize our queue in this way [OPTIONAL]
    // -------------------------------------------------------------------
    // queue<string> input_list({"A","+","(","B","*","C","-","(","D","/","E","^","F",")","*","G",")","*","H"});
    // queue<string> input_list({"A","+","B"}); // Simpler one!
    
    // Finally we can call our function solvePostfix and toPostfix
    // -------------------------------------------------------------------
    cout << solvePostfix(toPostfix(input_list)) << "\n";
    
    return 0;
}
```

{% hint style="info" %}
Example Input:

`4+ 2 ^ 2`

Example Output:

`8`
{% endhint %}
