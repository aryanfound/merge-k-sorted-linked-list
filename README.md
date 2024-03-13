# merge-k-sorted-linked-list
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* createnode();
struct ListNode* mergeKLists(struct ListNode** lists, int listsSize) {
    struct ListNode*head;
    if(listsSize==0)
    {
        return NULL;
    }
    struct ListNode* arr[listsSize];
    for(int i=0;i<listsSize;i++)
    {
        arr[i]=*(lists+i);

    }
    int temp=0;
    int max;
    int count;
    struct ListNode*dummy=(struct ListNode*)malloc(sizeof(struct ListNode));
    dummy->val=0;
    head=dummy;
    while(1)
    {
        max=INT_MAX;
        count=0;
        for(int i=0;i<listsSize;i++)
        {
        if(arr[i]==NULL)
        {
            count++;
        }
        else if(arr[i]->val<max)
        {
            max=arr[i]->val;
            temp=i;
        }
        }
        if(count==listsSize)
        {
            break;
        }
        struct ListNode*result=createnode();
        if(head!=NULL)
        {
        head->next=result;
        result->val=max;
        head=result;
        }
        if(arr[temp]!=NULL)
        {
        arr[temp]=arr[temp]->next;
        }
    }
    if(head==dummy)
    {
        return NULL;
    }
    return dummy->next;
}
struct ListNode* createnode()
{
    struct ListNode*temp=(struct ListNode*)malloc(sizeof(struct ListNode));
    temp->next=NULL;
    return temp;
}
