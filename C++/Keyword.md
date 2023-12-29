### `new`

General syntax : 

```c++
type *pointer_name = new type;
# px4 example
MulticopterRateControl *instance = new MulticopterRateControl(vtol);
```

```c++
#include <iostream>

int main() {
    // Allocate memory for an integer on the heap
    int *ptr_int = new int;

    // Allocate memory for an array of integers on the heap
    int *ptr_array = new int[5];

    // Assign values to the dynamically allocated memory
    *ptr_int = 42;

    for (int i = 0; i < 5; ++i) {
        ptr_array[i] = i * 10;
    }

    // Use the allocated memory
    std::cout << "Dynamically allocated integer: " << *ptr_int << std::endl;

    std::cout << "Dynamically allocated array elements: ";
    for (int i = 0; i < 5; ++i) {
        std::cout << ptr_array[i] << " ";
    }
    std::cout << std::endl;

    // Deallocate the memory to prevent memory leaks
    delete ptr_int;
    delete[] ptr_array;

    return 0;
}
```

