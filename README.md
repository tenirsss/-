#include<stdio.h>
#include<malloc.h>
struct node{
	int data;
	struct node *next;
};
int main(){
	int n,m;//n是总数，报数报到m时退出
	int answer[100]; //answer保存每次的答案，最后统一输出
	int count=0;//count用来控制题目答案的下标
	struct node *p,*q,*head,*tail;//p指向当前处理的节点， 
	head=(struct node *)malloc(sizeof(struct node));
	head->data=-1;
	head-> next=NULL;
	int i;
	while(1){
		scanf("%d%d",&n,&m);
		if(n==0||m==0){
			free(head);
			break;
		}
		else
		{
			tail=head;
			for(i=0;i<n;i++){
				p=(struct node *)malloc(sizeof(struct node));
				p->data=i+1;
				tail->next=p;//插到尾部
				p->next=head->next; 
				tail=p;
			}
			p=head->next;
			q=tail;
			i=1;
			while(p!=q){
				if(i==m){
					q->next=q->next->next;
					free(p);
					p=q->next;
					i=1;
				}
				else{
					q=p;
					p=p->next;
					i++;
				}
			}
			head->next=q;
			answer[count]=p->data;
			count++;
			free(p);
			head->next=NULL;
		}
	}
	for(i=0;i<count;i++){
		printf("%d\n",answer[i]);
		
	}
	free(head);
	
}
