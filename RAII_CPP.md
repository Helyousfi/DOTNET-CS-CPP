# Key Principles of RAII:
-  Initialization and Acquisition: Resources are acquired (allocated, opened, etc.) during object initialization (typically in the constructor).
-  Release and Cleanup: Resources are released (deallocated, closed, etc.) in the object's destructor, ensuring cleanup happens automatically when the object goes out of scope or is destroyed.
```
#include <iostream>
#include <vector>

// Example class using RAII for managing resources

class File {
public:
    explicit File(const char* filename) {
        file = fopen(filename, "r");
        if (!file) {
            throw std::runtime_error("Failed to open file");
        }
        std::cout << "File opened: " << filename << std::endl;
    }

    ~File() {
        if (file) {
            fclose(file);
            std::cout << "File closed" << std::endl;
        }
    }

    // Other member functions to read/write from the file

private:
    FILE* file;
};

int main() {
    try {
        File f("example.txt");
        // Use the file resource
        // When 'f' goes out of scope, the destructor is called
    } catch (const std::exception& e) {
        std::cerr << "Exception: " << e.what() << std::endl;
    }
    return 0;
}```


