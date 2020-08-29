# Interview-questions-2

4) Trees

i) Inorder traversal without recursion

#include<bits/stdc++.h> 
using namespace std; 

/* A binary tree Node has data, pointer to left child 
and a pointer to right child */
struct Node 
{ 
	int data; 
	struct Node* left; 
	struct Node* right; 
	Node (int data) 
	{ 
		this->data = data; 
		left = right = NULL; 
	} 
}; 

/* Iterative function for inorder tree 
traversal */
void inOrder(struct Node *root) 
{ 
	stack<Node *> s; 
	Node *curr = root; 

	while (curr != NULL || s.empty() == false) 
	{ 
		/* Reach the left most Node of the 
		curr Node */
		while (curr != NULL) 
		{ 
			/* place pointer to a tree node on 
			the stack before traversing 
			the node's left subtree */
			s.push(curr); 
			curr = curr->left; 
		} 

		/* Current must be NULL at this point */
		curr = s.top(); 
		s.pop(); 

		cout << curr->data << " "; 

		/* we have visited the node and its 
		left subtree. Now, it's right 
		subtree's turn */
		curr = curr->right; 

	} /* end of while */
} 

/* Driver program to test above functions*/
int main() 
{ 

	/* Constructed binary tree is 
			1 
			/ \ 
		2	 3 
		/ \ 
	4	 5 
	*/
	struct Node *root = new Node(1); 
	root->left	 = new Node(2); 
	root->right	 = new Node(3); 
	root->left->left = new Node(4); 
	root->left->right = new Node(5); 

	inOrder(root); 
	return 0; 
} 

ii) Preorder traversal without recursion

#include <bits/stdc++.h> 

using namespace std; 

/* A binary tree node has data, left child and right child */
struct node 
{ 
	int data; 
	struct node* left; 
	struct node* right; 
}; 

/* Helper function that allocates a new node with the given data and 
NULL left and right pointers.*/
struct node* newNode(int data) 
{ 
	struct node* node = new struct node; 
	node->data = data; 
	node->left = NULL; 
	node->right = NULL; 
	return(node); 
} 

// An iterative process to print preorder traversal of Binary tree 
void iterativePreorder(node *root) 
{ 
	// Base Case 
	if (root == NULL) 
	return; 

	// Create an empty stack and push root to it 
	stack<node *> nodeStack; 
	nodeStack.push(root); 

	/* Pop all items one by one. Do following for every popped item 
	a) print it 
	b) push its right child 
	c) push its left child 
	Note that right child is pushed first so that left is processed first */
	while (nodeStack.empty() == false) 
	{ 
		// Pop the top item from stack and print it 
		struct node *node = nodeStack.top(); 
		printf ("%d ", node->data); 
		nodeStack.pop(); 

		// Push right and left children of the popped node to stack 
		if (node->right) 
			nodeStack.push(node->right); 
		if (node->left) 
			nodeStack.push(node->left); 
	} 
} 

// Driver program to test above functions 
int main() 
{ 
	/* Constructed binary tree is 
			10 
		/ \ 
		8	 2 
	/ \ / 
	3	 5 2 
*/
struct node *root = newNode(10); 
root->left	 = newNode(8); 
root->right	 = newNode(2); 
root->left->left = newNode(3); 
root->left->right = newNode(5); 
root->right->left = newNode(2); 
iterativePreorder(root); 
return 0; 
}


iii) Left view of binary tree

#include <bits/stdc++.h> 
using namespace std; 

class node { 
public: 
	int data; 
	node *left, *right; 
}; 

// A utility function to create a new Binary Tree node 
node* newNode(int item) 
{ 
	node* temp = new node(); 
	temp->data = item; 
	temp->left = temp->right = NULL; 
	return temp; 
} 

// Recursive function to print left view of a binary tree. 
void leftViewUtil(node* root, int level, int* max_level) 
{ 
	// Base Case 
	if (root == NULL) 
		return; 

	// If this is the first node of its level 
	if (*max_level < level) { 
		cout << root->data << "\t"; 
		*max_level = level; 
	} 

	// Recur for left and right subtrees 
	leftViewUtil(root->left, level + 1, max_level); 
	leftViewUtil(root->right, level + 1, max_level); 
} 

// A wrapper over leftViewUtil() 
void leftView(node* root) 
{ 
	int max_level = 0; 
	leftViewUtil(root, 1, &max_level); 
} 

// Driver code 
int main() 
{ 
	node* root = newNode(12); 
	root->left = newNode(10); 
	root->right = newNode(30); 
	root->right->left = newNode(25); 
	root->right->right = newNode(40); 

	leftView(root); 

	return 0; 
} 

iv) Bottom view of Binary tree

#include<bits/stdc++.h> 
using namespace std; 

// Tree node class 
struct Node 
{ 
	int data; //data of the node 
	int hd; //horizontal distance of the node 
	Node *left, *right; //left and right references 

	// Constructor of tree node 
	Node(int key) 
	{ 
		data = key; 
		hd = INT_MAX; 
		left = right = NULL; 
	} 
}; 

// Method that prints the bottom view. 
void bottomView(Node *root) 
{ 
	if (root == NULL) 
		return; 

	// Initialize a variable 'hd' with 0 
	// for the root element. 
	int hd = 0; 

	// TreeMap which stores key value pair 
	// sorted on key value 
	map<int, int> m; 

	// Queue to store tree nodes in level 
	// order traversal 
	queue<Node *> q; 

	// Assign initialized horizontal distance 
	// value to root node and add it to the queue. 
	root->hd = hd; 
	q.push(root); // In STL, push() is used enqueue an item 

	// Loop until the queue is empty (standard 
	// level order loop) 
	while (!q.empty()) 
	{ 
		Node *temp = q.front(); 
		q.pop(); // In STL, pop() is used dequeue an item 

		// Extract the horizontal distance value 
		// from the dequeued tree node. 
		hd = temp->hd; 

		// Put the dequeued tree node to TreeMap 
		// having key as horizontal distance. Every 
		// time we find a node having same horizontal 
		// distance we need to replace the data in 
		// the map. 
		m[hd] = temp->data; 

		// If the dequeued node has a left child, add 
		// it to the queue with a horizontal distance hd-1. 
		if (temp->left != NULL) 
		{ 
			temp->left->hd = hd-1; 
			q.push(temp->left); 
		} 

		// If the dequeued node has a right child, add 
		// it to the queue with a horizontal distance 
		// hd+1. 
		if (temp->right != NULL) 
		{ 
			temp->right->hd = hd+1; 
			q.push(temp->right); 
		} 
	} 

	// Traverse the map elements using the iterator. 
	for (auto i = m.begin(); i != m.end(); ++i) 
		cout << i->second << " "; 
} 
 
int main() 
{ 
	Node *root = new Node(20); 
	root->left = new Node(8); 
	root->right = new Node(22); 
	root->left->left = new Node(5); 
	root->left->right = new Node(3); 
	root->right->left = new Node(4); 
	root->right->right = new Node(25); 
	root->left->right->left = new Node(10); 
	root->left->right->right = new Node(14); 
	cout << "Bottom view of the given binary tree :\n"
	bottomView(root); 
	return 0; 
} 




