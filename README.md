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

v) Top view of Binary Tree

#include <bits/stdc++.h> 
using namespace std; 

// Structure of binary tree 
struct Node 
{ 
	Node * left; 
	Node* right; 
	int hd; 
	int data; 
}; 

// function to create a new node 
Node* newNode(int key) 
{ 
	Node* node=new Node(); 
	node->left = node->right = NULL; 
	node->data=key; 
	return node; 
} 

// function should print the topView of 
// the binary tree 
void topview(Node* root) 
{ 
	if(root==NULL) 
	return; 
	queue<Node*>q; 
	map<int,int> m; 
	int hd=0; 
	root->hd=hd; 
	
	// push node and horizontal distance to queue 
	q.push(root); 
	
	cout<< "The top view of the tree is : \n"; 
	
	while(q.size()) 
	{ 
		hd=root->hd; 
		
		// count function returns 1 if the container 
		// contains an element whose key is equivalent 
		// to hd, or returns zero otherwise. 
		if(m.count(hd)==0) 
		m[hd]=root->data; 
		if(root->left) 
		{ 
			root->left->hd=hd-1; 
			q.push(root->left); 
		} 
		if(root->right) 
		{ 
			root->right->hd=hd+1; 
			q.push(root->right); 
		} 
		q.pop(); 
		root=q.front(); 
		
	} 
	
		
	for(auto i=m.begin();i!=m.end();i++) 
	{ 
		cout<<i->second<<" "; 
	} 
	
} 

int main() 
{ 
	
Node* root = newNode(1); 
	root->left = newNode(2); 
	root->right = newNode(3); 
	root->left->right = newNode(4); 
	root->left->right->right = newNode(5); 
	root->left->right->right->right = newNode(6); 
	cout<<"Following are nodes in top view of Binary Tree\n"; 
	topview(root); 
	return 0; 
} 

vi) Level order transversal in spiral form 


#include <iostream> 
#include <stack> 
using namespace std; 

// Binary Tree node 
struct node { 
	int data; 
	struct node *left, *right; 
}; 

void printSpiral(struct node* root) 
{ 
	if (root == NULL) 
		return; // NULL check 

	// Create two stacks to store alternate levels 
	stack<struct node*> s1; // For levels to be printed from right to left 
	stack<struct node*> s2; // For levels to be printed from left to right 

	// Push first level to first stack 's1' 
	s1.push(root); 

	// Keep printing while any of the stacks has some nodes 
	while (!s1.empty() || !s2.empty()) { 
		// Print nodes of current level from s1 and push nodes of 
		// next level to s2 
		while (!s1.empty()) { 
			struct node* temp = s1.top(); 
			s1.pop(); 
			cout << temp->data << " "; 

			// Note that is right is pushed before left 
			if (temp->right) 
				s2.push(temp->right); 
			if (temp->left) 
				s2.push(temp->left); 
		} 

		// Print nodes of current level from s2 and push nodes of 
		// next level to s1 
		while (!s2.empty()) { 
			struct node* temp = s2.top(); 
			s2.pop(); 
			cout << temp->data << " "; 

			// Note that is left is pushed before right 
			if (temp->left) 
				s1.push(temp->left); 
			if (temp->right) 
				s1.push(temp->right); 
		} 
	} 
} 

// A utility function to create a new node 
struct node* newNode(int data) 
{ 
	struct node* node = new struct node; 
	node->data = data; 
	node->left = NULL; 
	node->right = NULL; 

	return (node); 
} 

int main() 
{ 
	struct node* root = newNode(1); 
	root->left = newNode(2); 
	root->right = newNode(3); 
	root->left->left = newNode(7); 
	root->left->right = newNode(6); 
	root->right->left = newNode(5); 
	root->right->right = newNode(4); 
	cout << "Spiral Order traversal of binary tree is \n"; 
	printSpiral(root); 

	return 0; 
} 

vii) Height of  a binary tree

#include <bits/stdc++.h> 
using namespace std; 


/* A binary tree node has data, pointer to left child 
and a pointer to right child */
class node 
{ 
	public: 
	int data; 
	node* left; 
	node* right; 
}; 

/* Compute the "maxDepth" of a tree -- the number of 
	nodes along the longest path from the root node 
	down to the farthest leaf node.*/
int maxDepth(node* node) 
{ 
	if (node == NULL) 
		return 0; 
	else
	{ 
		/* compute the depth of each subtree */
		int lDepth = maxDepth(node->left); 
		int rDepth = maxDepth(node->right); 
	
		/* use the larger one */
		if (lDepth > rDepth) 
			return(lDepth + 1); 
		else return(rDepth + 1); 
	} 
} 

/* Helper function that allocates a new node with the 
given data and NULL left and right pointers. */
node* newNode(int data) 
{ 
	node* Node = new node(); 
	Node->data = data; 
	Node->left = NULL; 
	Node->right = NULL; 
	
	return(Node); 
} 
	 
int main() 
{ 
	node *root = newNode(1); 

	root->left = newNode(2); 
	root->right = newNode(3); 
	root->left->left = newNode(4); 
	root->left->right = newNode(5); 
	
	cout << "Height of tree is " << maxDepth(root); 
	return 0; 
} 

VIII) Diameter of a binary Tree
 
#include <bits/stdc++.h> 
using namespace std; 

/* Tree node structure used in the program */
struct Node { 
	int data; 
	Node* left, *right; 
}; 

/* Function to find height of a tree */
int height(Node* root, int& ans) 
{ 
	if (root == NULL) 
		return 0; 

	int left_height = height(root->left, ans); 

	int right_height = height(root->right, ans); 

	// update the answer, because diameter of a 
	// tree is nothing but maximum value of 
	// (left_height + right_height + 1) for each node 
	ans = max(ans, 1 + left_height + right_height); 

	return 1 + max(left_height, right_height); 
} 

/* Computes the diameter of binary tree with given root. */
int diameter(Node* root) 
{ 
	if (root == NULL) 
		return 0; 
	int ans = INT_MIN; // This will store the final answer 
	int height_of_tree = height(root, ans); 
	return ans; 
} 

struct Node* newNode(int data) 
{ 
	struct Node* node = new Node; 
	node->data = data; 
	node->left = node->right = NULL; 

	return (node); 
} 
 
int main() 
{ 
	struct Node* root = newNode(1); 
	root->left = newNode(2); 
	root->right = newNode(3); 
	root->left->left = newNode(4); 
	root->left->right = newNode(5); 

	printf("Diameter is %d\n", diameter(root)); 

	return 0; 
} 








