---
title: answer
date: 2023-01-10T20:45:48Z
lastmod: 2023-01-10T20:59:40Z
---

# answer

# Loops in the Linked List（链表判环）

```cpp
#include "Node.h"
bool check(node *head){
    node* slow=head;
    node* fast=head;
    while(fast && fast->next && fast->next->next){
        slow=slow->next;
        fast=fast->next->next;
        if(slow==fast){
            return true;
        }
    }
    return false;
}
```

## my answer

```cpp
#include<iostream>
#include "Node.h"
using namespace std;

// check if there exists a loop
bool check(node *head){
    node *fast=head;
    node *slow=head;
    while(fast!=slow){
        if(!fast||!fast->next){
            return false;
        }
        fast=fast->next->next;
        slow=slow->next;
    }
    return true;
}
```

‍

# Remove for single link list with head node

```cpp
#include "ListNode.h"
void List::remove(int pos){
    ListNode *p = head;
    for(int i = 1; i < pos; ++i){
        p = p->next;  
    }
    ListNode *temp = p->next;
    p->next = temp->next;
    delete temp;
}
```

## my answer

```cpp
#include "ListNode.h"

void List::remove(int pos)
{
    int flag=1;
    ListNode *cur=head;
    while(flag<pos){
        cur=cur->next;
        flag++;
    }
    cur->next=cur->next->next;
}
```

‍

# Insert for single link list with head node

```cpp
#include "ListNode.h"
void List::insert(int toadd, int pos) {
    ListNode *pre = head;
    if (pos <= 0) return;
    while (--pos && pre->next != NULL) {
        pre = pre->next;
    }
    ListNode * add = new ListNode;
    add->data = toadd;
    if (pre->next != NULL) {
        add->next = pre->next;
    } else {
        add->next = NULL;
    }
    pre->next = add;
}
```

## my answer

```cpp
#include "ListNode.h"

void List::insert(int toadd, int pos){
    int flag=1;
    ListNode *cur=head;
    while(flag<pos){
        cur=cur->next;
        flag++;
    }
    ListNode *ins=new ListNode;
    ins->data=toadd;
    ins->next=cur->next;
    cur->next=ins;
}
```

‍

# Delete Duplicate

```cpp
#include "LinkNode.h"
void delete_duplicate(LinkList &head)
{
	LinkList p = head;
	while(p && p -> next)
	{
		if(p -> data == p-> next -> data)
		{
			LinkList r = p -> next;
			p -> next = p -> next -> next;
			delete r;
		}
		else
			p = p -> next;
	}
}
```

## my answer

```cpp
#include "LinkNode.h"

void delete_duplicate(LinkList &head){
    LinkList p=head;
    if(p){
        while(p->next!=NULL){
            if(p->next->data==p->data){
                LinkList q=p->next;
                p->next=p->next->next;
                delete q;
            }
            else
                p=p->next;
        }    
    }

}
```

‍
