# Welcome to GitHub Desktop!

This is your README. READMEs are where you can communicate what your project is and how to use it.

Write your name on line 6, save it, and then head back to GitHub Desktop.
eihaku
#include <stdio.h>
#include <stdlib.h>

typedef struct _LIST{
    int data;
    struct _LIST *prev;
    struct _LIST *next;
}ST_LIST;

void dataListOutput(ST_LIST *pList);
void dataListFree(ST_LIST *pList);
ST_LIST *dataListCreate(int *arr, int length);
ST_LIST *dataListInster(ST_LIST *pList, int data);
ST_LIST *dataListDelete(ST_LIST *PList, int data);

int main(void)
{
    int arr[] = {11,22,33,44,55,66,77,88,99};
    int length;
    ST_LIST *pHead = NULL;
    
    length = sizeof(arr)/sizeof(int);
    pHead = dataListCreate(arr, length);
    pHead = dataListInster(pHead, 16);
    pHead - dataListDelete(pHead, 89);
    dataListOutput(pHead);
    dataListFree(pHead);
    printf("helle world");
    return EXIT_SUCCESS;
}
    ST_LIST *dataListDelete(ST_LIST *pList, int data){
        ST_LIST *pFirst = pList;
        if(pList != NULL){
            if(pList->data == data){
                pFirst =pList->next;
                pList->next->prev = NULL;
                free(pList);
                return pFirst;
            }
        }
        
        while(pList != NULL){
            if(pList->data==data){
                pList->prev->next = pList->next;
                if(pList->next){
                    pList->next->prev = pList->prev;
                }
                free(pList);
                break;
            }else{
                pList = pList->next;
            }
        }
        return pFirst;
    }




    ST_LIST *dataListInster(ST_LIST *pList, int data){
        ST_LIST *pFirst = pList;
        ST_LIST *pTemp;
        
        pTemp= (ST_LIST*)malloc(sizeof(ST_LIST));
        pTemp->data = data;
        
        if(pList->data >= data){
            pTemp->next = pList;
            pTemp->prev = NULL;
            pList->prev = pTemp;
            return pTemp;
        }
        while(pList!=NULL){
            if(pList->data >=data){
                pTemp->next = pList;
                pTemp->prev = pList->prev;
                pList->prev = pTemp;
                break;
            }
            else{
                    if(pList->next){
                        pList = pList->next;
                    }else{
                        
                        pList->next = pTemp;
                        pTemp->next = NULL;
                        pTemp->prev = pList;
                        break;
                }
            }
        }
        return pFirst;
    }
    
    ST_LIST *dataListCreate(int *arr, int length) {
        ST_LIST *pTemp;
        ST_LIST *pCurrent;
        ST_LIST *pList = NULL;
        
        pList = (ST_LIST*)malloc(sizeof(ST_LIST));
        pList->data = arr[0];
        pList->prev = NULL;
        pList->next = NULL;
        pCurrent = pList;
        
        for(int i=1; i<length; i++){
            pTemp = (ST_LIST*)malloc(sizeof(ST_LIST));
            pTemp->data = arr[i];
            pTemp->prev = NULL;
            pTemp->next = NULL;
            
            pTemp->prev = pCurrent;
            pCurrent->next = pTemp;
            pCurrent = pTemp;
        }
        return pList;
    }
    
    
    void dataListFree(ST_LIST *pList){
        ST_LIST *pTemp = pList;
        while(pList != NULL){
            pTemp = pList->next;
            free(pList);
            pList = pTemp;
        }
    }
    void dataListOutput(ST_LIST *pList){
        int count = 1;
        while(pList != NULL){
            printf("%2d %4d P:%p [%p] N:%p \n",  count++, pList->data, pList->prev, pList, pList->next);
            pList = pList->next;
        }
    }
    

