### Callback

refers to a function or a code snippet that is passed as an argument to another function.

```c++
#include <iostream>

// Callback function type
typedef void (*CallbackFunction)();

// Function with a callback parameter
void performOperation(CallbackFunction callback) {
    // Perform some operation
    std::cout << "Performing operation..." << std::endl;

    // Invoke the callback
    callback();
}

// Callback function
void myCallback() {
    std::cout << "Callback function called!" << std::endl;
}

int main() {
    // Using the callback
    performOperation(myCallback);

    return 0;
}
```

### Event

A mechanism used to signal that a specific occurrence has taken place within a program



In C++, events are often implemented using observer patterns, where one  part of the program (subject) triggers events, and other parts  (observers) respond to those events.



Can be used with Callback, a callback is executed when an event is triggered.



```c++
#include <iostream>
#include <vector>

// Event class
class Event {
public:
    // Callback function type
    typedef void (*CallbackFunction)();

    // Subscribe to the event
    void subscribe(CallbackFunction callback) {
        callbacks.push_back(callback);
    }

    // Trigger the event
    void trigger() {
        for (auto& callback : callbacks) {
            callback();
        }
    }

private:
    std::vector<CallbackFunction> callbacks;
};

// Callback function
void myCallback() {
    std::cout << "Event occurred! Callback function called!" << std::endl;
}

int main() {
    // Create an event
    Event myEvent;

    // Subscribe the callback to the event
    myEvent.subscribe(myCallback);

    // Trigger the event
    myEvent.trigger();

    return 0;
}
```

