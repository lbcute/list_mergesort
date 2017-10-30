```#include<iostream>
using namespace std;
struct listNode//利用结构构建链表
{
  int val;
  listNode* next;
};
class mergeSort//归并排序
{public:
  void insert(listNode* & head)//依次插入数据
  { cout<<"请输入任意数据创建链表(以0结束输入)："<<endl;
    listNode *s,*p;
    s=new listNode;
    cin>>s->val;
    while(s->val!=0)
    {
      if(head==NULL)
        head=s;
      else
        p->next=s;
        p=s;
      s=new listNode;
      cin>>s->val;
 }
  }
  void printList(listNode* head)//输出链表
  {
   cout<<"链表数据从小到大排列依次为："<<endl;
   while(head)
   {
     cout<<head->val<<" ";
     head=head->next;
  }
  cout<<endl;
  }
  listNode* getMid(listNode* head)//返回链表中间位置的指针，将链表一分为二
  {
    if(head==NULL||head->next==NULL)//链表中没有元素或者只有一个元素时,将头指针>返回
      return head;
    listNode* l1=head;//l1初始化为头指针
    listNode* l2=head->next;//l2初始化为头指针的next指针
    while(l2&&l2->next)
    {
      l1=l1->next;
      l2=l2->next->next;//l2还没到链表尾部时，l2每次向后移动两个位置，l1每次向后移动一个位置

    }
    return l1;//当l2到达表尾时，l1指向链表的中间位置
  }
listNode* sortList(listNode* & head)
  {
    if(head==NULL||head->next==NULL)
      return head;//只有一个值或者没有值时，直接将头指针返回
    listNode* mid=getMid(head);//mid表示中间位置
    listNode* right=NULL;

    if(mid!=NULL)
    {
      right=mid->next;//用right表示右边半个表的头指针
}
    mid->next=NULL;

    sortList(head);//递归，分而治之
    sortList(right);
    head=merge(head,right);//将左右表合并

    return head;
}
  listNode* merge(listNode* left,listNode* right)
  {
    if(left==NULL)
      return right;
    if(right==NULL)
      return left;
    listNode* p=right;
    while(p)
    {
      listNode* l=left,*lp=NULL;
      while(l&&l->val<p->val)
      {
	if(!lp)
	  lp=left;
	else
	  lp=lp->next;
	l=l->next;
      }
      listNode* tmp=p->next;
     /* if(l)
      {lp->next=p;
	p->next=l;
      }
      else
      {left=p;}
      p=tmp;*/
     if(lp)
       lp->next=p;
     else
       left=p;
     p->next=l;
     p=tmp;
    }
     
    return left;
  }


};
int main()
{
  listNode* head=NULL;
  mergeSort s;

  s.insert(head);
  s.sortList(head);
  s.printList(head);

}
```
