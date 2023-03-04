# 实现一个简单point类

```cpp
class point{
	public:
		point(double x=0,double y=0){
			this->x=x;
			this->y=y;
			count++;
		}
		static int count;
		void print(){
			std::cout<<'('<<x<<','<<y<<')'<<std::endl;
		}
		bool judge(const point &p1,const point &p2){
			double dx1=p1.x-x;
			double dx2=p2.x-x;
			double dy1=p1.y-y;
			double dy2=p2.y-y;
			if(dx1==0&&dx2==0){
				return true;
			}
			else if(dx1==0||dx2==0){
				return false;
			}
			else if(dy1/dx1==dy2/dx2){
				return true;
			}
			else{
				return false;
			}
		}
	private:
		double x;
		double y;
};
int point::count=0;

```

## my answer

```cpp
#include <iostream>
using namespace std;

class point{
public:
    static int count;
    double x=0;
    double y=0;
    point(double x_,double y_):x(x_),y(y_){
        count++;
    }
    ~point(){
        count--;
    }
    void print(){
        cout<<'('<<x<<','<<y<<')'<<endl;
    }
    bool judge(point& p1,point& p2){
        return (p1.y-y)/(p1.x-x)==(p2.y-y)/(p2.x-x);
    }
};
int point::count=0;
```

‍
