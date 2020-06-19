# Reverse Nodes In K Group

Inverse the whole list
Inverse in K-group aligning from the leftmost
Inverse in K-group aligning from the rightmost

```
#include<string>
#include<iostream>
#include<vector>
#include<climits>
#include<random>
#include<ctime>
#include<cassert>

using namespace std;

struct TreeNode {
    int val;
    TreeNode* next;

    TreeNode(int x) : val(x), next(nullptr) {}
};

TreeNode* reverseNodes(TreeNode* node) {
    if (node == nullptr || node->next == nullptr) return node;

    TreeNode* next = node->next;
    TreeNode* newRoot = reverseNodes(node->next);
    next->next = node;
    node->next = nullptr;
    return  newRoot;
}

TreeNode* forwardReverse(TreeNode* root, int k) {
    TreeNode* temp = root;

    for (int i = 1; i < k && temp != nullptr; i++) {
        temp = temp->next;
    }
    if (temp == nullptr) {
        return root;
    }

    TreeNode* nextNode = temp->next;
    temp->next = nullptr;
    TreeNode* rightHalf = forwardReverse(nextNode, k);
    TreeNode* leftHalf = reverseNodes(root);
    root->next = rightHalf;
    return leftHalf;
}

TreeNode* backwardReverse(TreeNode* root, int k) {
    root = reverseNodes(root);
    root = forwardReverse(root, k);

    return reverseNodes(root);
}

int main() {
    srand(time(NULL));
    TreeNode head(rand()%10);
    TreeNode* root = &head;
    for(int i = 0; i < 5; i++) {
        root->next = new TreeNode(rand()%10);
        root = root->next;
    }

    root = &head;
    while (root != nullptr) {
        cout << root->val << " ";
        root = root->next;
    }
    cout << endl;

    root = &head;
    root = backwardReverse(root,4);
    while (root != nullptr) {
        cout << root->val << " ";
        root = root->next;
    }
    cout << endl;

    return 0;
}
```
