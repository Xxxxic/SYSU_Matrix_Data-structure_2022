## official answer

```cpp
// Problem#: 17815
// Submission#: 4605229
// The source code is licensed under Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported License
// URI: http://creativecommons.org/licenses/by-nc-sa/3.0/
// All Copyright reserved by Informatic Lab of Sun Yat-sen University
//#include "Object.h"
void TestObjects() {
	Object *o1;
	Object *o2;
	Object *o3;
	Object *o4;
	o1 = new Object(1);
	o2 = new Object(2);
	o3 = new Object(3);
	delete o3;
	delete o2;
	o4 = new Object(4);
	delete o4;
	delete o1;
}
```

## my answer

```cpp
#include <iostream>
//#include "Object.h"
using namespace std;
void TestObjects(){
    Object* i1=new Object(1);
    Object* i2=new Object(2);
    Object* i3=new Object(3);
    delete i3;
    delete i2;
    Object* i4=new Object(4);
    delete i4;
    delete i1;
}
```

‍