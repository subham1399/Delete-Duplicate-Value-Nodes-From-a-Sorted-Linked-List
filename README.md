# Delete-Duplicate-Value-Nodes-From-a-Sorted-Linked-List @Hackerrank#CPP+14
Question Description:
You're given the pointer to the head node of a sorted linked list, where the data in the nodes is in ascending order. 
Delete as few nodes as possible so that the list does not contain any value more than once. 
The given head pointer may be null indicating that the list is empty.

Input Formats:
You have to complete the SinglyLinkedListNode* removeDuplicates(SinglyLinkedListNode* head) method which takes one argument - the head of the sorted linked list. You should NOT read any input from stdin/console.

The input is handled by the code in the editor and the format is as follows:

The first line contains an integer , denoting the number of test cases. The format for each test case is as follows:

The first line contains an integer , denoting the number of elements in the linked list. 
The next  lines contain an integer each, denoting the elements of the linked list.

Output Format:
Delete as few nodes as possible to ensure that no two nodes have the same data. 
Adjust the next pointers to ensure that the remaining nodes form a single sorted linked list.
Then return the head of the sorted updated linked list. Do NOT print anything to stdout/console.

The output is handled by the code in the editor and the format is as follows:
For each test case, print in a new line, the data of the linked list after removing the duplicates separated by space.


Code:

#include <bits/stdc++.h>

using namespace std;

class SinglyLinkedListNode {
    public:
        int data;
        SinglyLinkedListNode *next;

        SinglyLinkedListNode(int node_data) {
            this->data = node_data;
            this->next = nullptr;
        }
};

class SinglyLinkedList {
    public:
        SinglyLinkedListNode *head;
        SinglyLinkedListNode *tail;

        SinglyLinkedList() {
            this->head = nullptr;
            this->tail = nullptr;
        }

        void insert_node(int node_data) {
            SinglyLinkedListNode* node = new SinglyLinkedListNode(node_data);

            if (!this->head) {
                this->head = node;
            } else {
                this->tail->next = node;
            }

            this->tail = node;
        }
};

void print_singly_linked_list(SinglyLinkedListNode* node, string sep, ofstream& fout) {
    while (node) {
        fout << node->data;

        node = node->next;

        if (node) {
            fout << sep;
        }
    }
}

void free_singly_linked_list(SinglyLinkedListNode* node) {
    while (node) {
        SinglyLinkedListNode* temp = node;
        node = node->next;

        free(temp);
    }
}

// Complete the removeDuplicates function below.

/*
 * For your reference:
 *
 * SinglyLinkedListNode {
 *     int data;
 *     SinglyLinkedListNode* next;
 * };
 *
 */
SinglyLinkedListNode* removeDuplicates(SinglyLinkedListNode* head) {


SinglyLinkedListNode *cur = head;
    int last_seen = cur->data;
    while(cur->next) {
        if(cur->next->data == last_seen) {
            cur->next = cur->next->next;
        }else {
            cur = cur->next;
            last_seen = cur->data;
        }
    }
    return head;
}

int main()
{
    ofstream fout(getenv("OUTPUT_PATH"));

    int t;
    cin >> t;
    cin.ignore(numeric_limits<streamsize>::max(), '\n');

    for (int t_itr = 0; t_itr < t; t_itr++) {
        SinglyLinkedList* llist = new SinglyLinkedList();

        int llist_count;
        cin >> llist_count;
        cin.ignore(numeric_limits<streamsize>::max(), '\n');

        for (int i = 0; i < llist_count; i++) {
            int llist_item;
            cin >> llist_item;
            cin.ignore(numeric_limits<streamsize>::max(), '\n');

            llist->insert_node(llist_item);
        }

        SinglyLinkedListNode* llist1 = removeDuplicates(llist->head);

        print_singly_linked_list(llist1, " ", fout);
        fout << "\n";

        free_singly_linked_list(llist1);
    }

    fout.close();

    return 0;
}



