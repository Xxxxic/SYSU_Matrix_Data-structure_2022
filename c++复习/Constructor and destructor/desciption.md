# Constructor and destructor

## Description

Given the following Object class implemetation, write a function to produce the desired output. No changes should be made with the Object class.

```cpp
class Object {
public:
    Object(int i) {
        id = i;
        count++;
        cout<<"Object "<<id<<" is created, we've got "<<count<<" object(s) now!"<<endl;
    }
    ~Object() { 
        count--;
        cout<<"Object "<<id<<" is deleted, we've got "<<count<<" object(s) now!"<<endl;
    }
private:
    int id;
    static int count;
};
int Object::count = 0;


 int main()
{
    TestObjects();
    return 0;
}
```

## Output

Output should just be produced by the constructor and destructor of the Object class.

## Sample Output

```
Object 1 is created, we've got 1 object(s) now!
Object 2 is created, we've got 2 object(s) now!
Object 3 is created, we've got 3 object(s) now!
Object 3 is deleted, we've got 2 object(s) now!
Object 2 is deleted, we've got 1 object(s) now!
Object 4 is created, we've got 2 object(s) now!
Object 4 is deleted, we've got 1 object(s) now!
Object 1 is deleted, we've got 0 object(s) now!
```

main.cpp：

```cpp
#include <iostream>
using namespace std;

class Object {
public:
    Object(int i) {
        id = i;
        count++;
        cout<<"Object "<<id<<" is created, we've got "<<count<<" object(s) now!"<<endl;
    }
    ~Object() {
        count--;
        cout<<"Object "<<id<<" is deleted, we've got "<<count<<" object(s) now!"<<endl;
    }
private:
    int id;
    static int count;
};
int Object::count = 0;

int main()
{
  	TestObjects();
    return 0;
}
```