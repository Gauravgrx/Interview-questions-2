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

ix) Check if the binary tree is height balanced

#include <bits/stdc++.h> 
using namespace std; 

/* A binary tree node has data, 
pointer to left child and 
a pointer to right child */
class node { 
public: 
	int data; 
	node* left; 
	node* right; 
}; 

/* Returns the height of a binary tree */
int height(node* node); 

/* Returns true if binary tree 
with root as root is height-balanced */
bool isBalanced(node* root) 
{ 
	int lh; /* for height of left subtree */
	int rh; /* for height of right subtree */

	/* If tree is empty then return true */
	if (root == NULL) 
		return 1; 

	/* Get the height of left and right sub trees */
	lh = height(root->left); 
	rh = height(root->right); 

	if (abs(lh - rh) <= 1 && isBalanced(root->left) && isBalanced(root->right)) 
		return 1; 

	/* If we reach here then 
	tree is not height-balanced */
	return 0; 
} 

/* UTILITY FUNCTIONS TO TEST isBalanced() FUNCTION */

/* returns maximum of two integers */
int max(int a, int b) 
{ 
	return (a >= b) ? a : b; 
} 

/* The function Compute the "height" 
of a tree. Height is the number of 
nodes along the longest path from 
the root node down to the farthest leaf node.*/
int height(node* node) 
{ 
	/* base case tree is empty */
	if (node == NULL) 
		return 0; 

	/* If tree is not empty then 
	height = 1 + max of left 
		height and right heights */
	return 1 + max(height(node->left), 
				height(node->right)); 
} 

/* Helper function that allocates 
a new node with the given data 
and NULL left and right pointers. */
node* newNode(int data) 
{ 
	node* Node = new node(); 
	Node->data = data; 
	Node->left = NULL; 
	Node->right = NULL; 

	return (Node); 
} 


int main() 
{ 
	node* root = newNode(1); 
	root->left = newNode(2); 
	root->right = newNode(3); 
	root->left->left = newNode(4); 
	root->left->right = newNode(5); 
	root->left->left->left = newNode(8); 

	if (isBalanced(root)) 
		cout << "Tree is balanced"; 
	else
		cout << "Tree is not balanced"; 
	return 0; 
}  

x) LCA in binary tree

#include <iostream> 
#include <vector> 

using namespace std; 

// A Binary Tree node 
struct Node 
{ 
	int key; 
	struct Node *left, *right; 
}; 

// Utility function creates a new binary tree node with given key 
Node * newNode(int k) 
{ 
	Node *temp = new Node; 
	temp->key = k; 
	temp->left = temp->right = NULL; 
	return temp; 
} 

// Finds the path from root node to given root of the tree, Stores the 
// path in a vector path[], returns true if path exists otherwise false 
bool findPath(Node *root, vector<int> &path, int k) 
{ 
	// base case 
	if (root == NULL) return false; 

	// Store this node in path vector. The node will be removed if 
	// not in path from root to k 
	path.push_back(root->key); 

	// See if the k is same as root's key 
	if (root->key == k) 
		return true; 

	// Check if k is found in left or right sub-tree 
	if ( (root->left && findPath(root->left, path, k)) || 
		(root->right && findPath(root->right, path, k)) ) 
		return true; 

	// If not present in subtree rooted with root, remove root from 
	// path[] and return false 
	path.pop_back(); 
	return false; 
} 

// Returns LCA if node n1, n2 are present in the given binary tree, 
// otherwise return -1 
int findLCA(Node *root, int n1, int n2) 
{ 
	// to store paths to n1 and n2 from the root 
	vector<int> path1, path2; 

	// Find paths from root to n1 and root to n1. If either n1 or n2 
	// is not present, return -1 
	if ( !findPath(root, path1, n1) || !findPath(root, path2, n2)) 
		return -1; 

	/* Compare the paths to get the first different value */
	int i; 
	for (i = 0; i < path1.size() && i < path2.size() ; i++) 
		if (path1[i] != path2[i]) 
			break; 
	return path1[i-1]; 
} 

int main() 
{ 
 
	Node * root = newNode(1); 
	root->left = newNode(2); 
	root->right = newNode(3); 
	root->left->left = newNode(4); 
	root->left->right = newNode(5); 
	root->right->left = newNode(6); 
	root->right->right = newNode(7); 
	cout << "LCA(4, 5) = " << findLCA(root, 4, 5); 
	cout << "nLCA(4, 6) = " << findLCA(root, 4, 6); 
	cout << "nLCA(3, 4) = " << findLCA(root, 3, 4); 
	cout << "nLCA(2, 4) = " << findLCA(root, 2, 4); 
	return 0; 
} 


xi)  Check if two binary trees are indentical or not

 
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

/* Given two trees, return true if they are 
structurally identical */
int identicalTrees(node* a, node* b) 
{ 
	/*1. both empty */
	if (a == NULL && b == NULL) 
		return 1; 

	/* 2. both non-empty -> compare them */
	if (a != NULL && b != NULL) 
	{ 
		return
		( 
			a->data == b->data && 
			identicalTrees(a->left, b->left) && 
			identicalTrees(a->right, b->right) 
		); 
	} 
	
	/* 3. one empty, one not -> false */
	return 0; 
} 

int main() 
{ 
	node *root1 = newNode(1); 
	node *root2 = newNode(1); 
	root1->left = newNode(2); 
	root1->right = newNode(3); 
	root1->left->left = newNode(4); 
	root1->left->right = newNode(5); 

	root2->left = newNode(2); 
	root2->right = newNode(3); 
	root2->left->left = newNode(4); 
	root2->left->right = newNode(5); 

	if(identicalTrees(root1, root2)) 
		cout << "Both tree are identical."; 
	else
		cout << "Trees are not identical."; 

return 0; 
} 

x) Maximmum path sum in binary tree


#include<bits/stdc++.h> 
using namespace std; 

// A binary tree node 
struct Node 
{ 
	int data; 
	struct Node* left, *right; 
}; 

// A utility function to allocate a new node 
struct Node* newNode(int data) 
{ 
	struct Node* newNode = new Node; 
	newNode->data = data; 
	newNode->left = newNode->right = NULL; 
	return (newNode); 
} 

// This function returns overall maximum path sum in 'res' 
// And returns max path sum going through root. 
int findMaxUtil(Node* root, int &res) 
{ 
	//Base Case 
	if (root == NULL) 
		return 0; 

	// l and r store maximum path sum going through left and 
	// right child of root respectively 
	int l = findMaxUtil(root->left,res); 
	int r = findMaxUtil(root->right,res); 

	// Max path for parent call of root. This path must 
	// include at-most one child of root 
	int max_single = max(max(l, r) + root->data, root->data); 

	// Max Top represents the sum when the Node under 
	// consideration is the root of the maxsum path and no 
	// ancestors of root are there in max sum path 
	int max_top = max(max_single, l + r + root->data); 

	res = max(res, max_top); // Store the Maximum Result. 

	return max_single; 
} 

// Returns maximum path sum in tree with given root 
int findMaxSum(Node *root) 
{ 
	// Initialize result 
	int res = INT_MIN; 

	// Compute and return result 
	findMaxUtil(root, res); 
	return res; 
} 


int main(void) 
{ 
	struct Node *root = newNode(10); 
	root->left	 = newNode(2); 
	root->right	 = newNode(10); 
	root->left->left = newNode(20); 
	root->left->right = newNode(1); 
	root->right->right = newNode(-25); 
	root->right->right->left = newNode(3); 
	root->right->right->right = newNode(4); 
	cout << "Max path sum is " << findMaxSum(root); 
	return 0; 
} 

xi) Create binary tree from inorder and preorder transveral


#include <bits/stdc++.h> 
using namespace std; 

/* A binary tree node has data, pointer to left child 
and a pointer to right child */
class node 
{ 
	public: 
	char data; 
	node* left; 
	node* right; 
}; 

/* Prototypes for utility functions */
int search(char arr[], int strt, int end, char value); 
node* newNode(char data); 

/* Recursive function to construct binary 
of size len from Inorder traversal in[] 
and Preorder traversal pre[]. Initial values 
of inStrt and inEnd should be 0 and len -1. 
The function doesn't do any error checking 
for cases where inorder and preorder do not 
form a tree */
node* buildTree(char in[], char pre[], int inStrt, int inEnd) 
{ 
	static int preIndex = 0; 

	if (inStrt > inEnd) 
		return NULL; 

	/* Pick current node from Preorder 
	traversal using preIndex 
	and increment preIndex */
	node* tNode = newNode(pre[preIndex++]); 

	/* If this node has no children then return */
	if (inStrt == inEnd) 
		return tNode; 

	/* Else find the index of this node in Inorder traversal */
	int inIndex = search(in, inStrt, inEnd, tNode->data); 

	/* Using index in Inorder traversal, construct left and 
	right subtress */
	tNode->left = buildTree(in, pre, inStrt, inIndex - 1); 
	tNode->right = buildTree(in, pre, inIndex + 1, inEnd); 

	return tNode; 
} 

/* UTILITY FUNCTIONS */
/* Function to find index of value in arr[start...end] 
The function assumes that value is present in in[] */
int search(char arr[], int strt, int end, char value) 
{ 
	int i; 
	for (i = strt; i <= end; i++) 
	{ 
		if (arr[i] == value) 
			return i; 
	} 
} 

/* Helper function that allocates a new node with the 
given data and NULL left and right pointers. */
node* newNode(char data) 
{ 
	node* Node = new node(); 
	Node->data = data; 
	Node->left = NULL; 
	Node->right = NULL; 

	return (Node); 
} 

/* This funtcion is here just to test buildTree() */
void printInorder(node* node) 
{ 
	if (node == NULL) 
		return; 

	/* first recur on left child */
	printInorder(node->left); 

	/* then print the data of node */
	cout<<node->data<<" "; 

	/* now recur on right child */
	printInorder(node->right); 
} 

int main() 
{ 
	char in[] = { 'D', 'B', 'E', 'A', 'F', 'C' }; 
	char pre[] = { 'A', 'B', 'D', 'E', 'C', 'F' }; 
	int len = sizeof(in) / sizeof(in[0]); 
	node* root = buildTree(in, pre, 0, len - 1); 

	/* Let us test the built tree by 
	printing Insorder traversal */
	cout << "Inorder traversal of the constructed tree is \n"; 
	printInorder(root); 
} 


xii) Symmetric Binary Tree

 
#include<bits/stdc++.h> 
using namespace std; 

// A Binary Tree Node 
struct Node 
{ 
	int key; 
	struct Node* left, *right; 
}; 

// Utility function to create new Node 
Node *newNode(int key) 
{ 
	Node *temp = new Node; 
	temp->key = key; 
	temp->left = temp->right = NULL; 
	return (temp); 
} 

// Returns true if trees with roots as root1 and root2 are mirror 
bool isMirror(struct Node *root1, struct Node *root2) 
{ 
	// If both trees are emptu, then they are mirror images 
	if (root1 == NULL && root2 == NULL) 
		return true; 

	// For two trees to be mirror images, the following three 
	// conditions must be true 
	// 1 - Their root node's key must be same 
	// 2 - left subtree of left tree and right subtree 
	//	 of right tree have to be mirror images 
	// 3 - right subtree of left tree and left subtree 
	//	 of right tree have to be mirror images 
	if (root1 && root2 && root1->key == root2->key) 
		return isMirror(root1->left, root2->right) && 
			isMirror(root1->right, root2->left); 

	// if neither of above conditions is true then root1 
	// and root2 are not mirror images 
	return false; 
} 

// Returns true if a tree is symmetric i.e. mirror image of itself 
bool isSymmetric(struct Node* root) 
{ 
	// Check if tree is mirror of itself 
	return isMirror(root, root); 
} 

int main() 
{ 
	// Let us construct the Tree shown in the above figure 
	Node *root	 = newNode(1); 
	root->left	 = newNode(2); 
	root->right	 = newNode(2); 
	root->left->left = newNode(3); 
	root->left->right = newNode(4); 
	root->right->left = newNode(4); 
	root->right->right = newNode(3); 

	cout << isSymmetric(root); 
	return 0; 
} 


xiii)  Flatten binary tree to linkedlist 


#include <iostream> 
using namespace std; 

struct Node { 
	int key; 
	Node *left, *right; 
}; 

/* utility that allocates a new Node 
with the given key */
Node* newNode(int key) 
{ 
	Node* node = new Node; 
	node->key = key; 
	node->left = node->right = NULL; 
	return (node); 
} 

// Function to convert binary tree into 
// linked list by altering the right node 
// and making left node point to NULL 
void flatten(struct Node* root) 
{ 
	// base condition- return if root is NULL 
	// or if it is a leaf node 
	if (root == NULL || root->left == NULL && 
						root->right == NULL) { 
		return; 
	} 

	// if root->left exists then we have 
	// to make it root->right 
	if (root->left != NULL) { 

		// move left recursively 
		flatten(root->left); 
	
		// store the node root->right 
		struct Node* tmpRight = root->right; 
		root->right = root->left; 
		root->left = NULL; 

		// find the position to insert 
		// the stored value 
		struct Node* t = root->right; 
		while (t->right != NULL) { 
			t = t->right; 
		} 

		// insert the stored value 
		t->right = tmpRight; 
	} 

	// now call the same function 
	// for root->right 
	flatten(root->right); 
} 

// To find the inorder traversal 
void inorder(struct Node* root) 
{ 
	// base condition 
	if (root == NULL) 
		return; 
	inorder(root->left); 
	cout << root->key << " "; 
	inorder(root->right); 
} 

int main() 
{ 
	/* 1 
		/ \ 
	2	 5 
	/ \	 \ 
	3 4	 6 */
	Node* root = newNode(1); 
	root->left = newNode(2); 
	root->right = newNode(5); 
	root->left->left = newNode(3); 
	root->left->right = newNode(4); 
	root->right->right = newNode(6); 

	flatten(root); 

	cout << "The Inorder traversal after "
			"flattening binary tree "; 
	inorder(root); 
	return 0; 
} 


xiv)  Check if binary tree is mirror of itself or not

    Same as xii) i.e symmetric binary tree
    

5) GRAPH

i) DFS

 
#include<bits/stdc++.h> 
using namespace std; 

// Graph class represents a directed graph 
// using adjacency list representation 
class Graph 
{ 
	int V; // No. of vertices 

	// Pointer to an array containing 
	// adjacency lists 
	list<int> *adj; 

	// A recursive function used by DFS 
	void DFSUtil(int v, bool visited[]); 
public: 
	Graph(int V); // Constructor 

	// function to add an edge to graph 
	void addEdge(int v, int w); 

	// DFS traversal of the vertices 
	// reachable from v 
	void DFS(int v); 
}; 

Graph::Graph(int V) 
{ 
	this->V = V; 
	adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
	adj[v].push_back(w); // Add w to v’s list. 
} 

void Graph::DFSUtil(int v, bool visited[]) 
{ 
	// Mark the current node as visited and 
	// print it 
	visited[v] = true; 
	cout << v << " "; 

	// Recur for all the vertices adjacent 
	// to this vertex 
	list<int>::iterator i; 
	for (i = adj[v].begin(); i != adj[v].end(); ++i) 
		if (!visited[*i]) 
			DFSUtil(*i, visited); 
} 

// DFS traversal of the vertices reachable from v. 
// It uses recursive DFSUtil() 
void Graph::DFS(int v) 
{ 
	// Mark all the vertices as not visited 
	bool *visited = new bool[V]; 
	for (int i = 0; i < V; i++) 
		visited[i] = false; 

	// Call the recursive helper function 
	// to print DFS traversal 
	DFSUtil(v, visited); 
} 


int main() 
{ 
	// Create a graph given in the above diagram 
	Graph g(4); 
	g.addEdge(0, 1); 
	g.addEdge(0, 2); 
	g.addEdge(1, 2); 
	g.addEdge(2, 0); 
	g.addEdge(2, 3); 
	g.addEdge(3, 3); 

	cout << "Following is Depth First Traversal"
			" (starting from vertex 2) \n"; 
	g.DFS(2); 

	return 0; 
} 

ii) BFS


#include<iostream> 
#include <list> 

using namespace std; 

// This class represents a directed graph using 
// adjacency list representation 
class Graph 
{ 
	int V; // No. of vertices 

	// Pointer to an array containing adjacency 
	// lists 
	list<int> *adj; 
public: 
	Graph(int V); // Constructor 

	// function to add an edge to graph 
	void addEdge(int v, int w); 

	// prints BFS traversal from a given source s 
	void BFS(int s); 
}; 

Graph::Graph(int V) 
{ 
	this->V = V; 
	adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
	adj[v].push_back(w); // Add w to v’s list. 
} 

void Graph::BFS(int s) 
{ 
	// Mark all the vertices as not visited 
	bool *visited = new bool[V]; 
	for(int i = 0; i < V; i++) 
		visited[i] = false; 

	// Create a queue for BFS 
	list<int> queue; 

	// Mark the current node as visited and enqueue it 
	visited[s] = true; 
	queue.push_back(s); 

	// 'i' will be used to get all adjacent 
	// vertices of a vertex 
	list<int>::iterator i; 

	while(!queue.empty()) 
	{ 
		// Dequeue a vertex from queue and print it 
		s = queue.front(); 
		cout << s << " "; 
		queue.pop_front(); 

		// Get all adjacent vertices of the dequeued 
		// vertex s. If a adjacent has not been visited, 
		// then mark it visited and enqueue it 
		for (i = adj[s].begin(); i != adj[s].end(); ++i) 
		{ 
			if (!visited[*i]) 
			{ 
				visited[*i] = true; 
				queue.push_back(*i); 
			} 
		} 
	} 
} 

 
int main() 
{ 
	// Create a graph given in the above diagram 
	Graph g(4); 
	g.addEdge(0, 1); 
	g.addEdge(0, 2); 
	g.addEdge(1, 2); 
	g.addEdge(2, 0); 
	g.addEdge(2, 3); 
	g.addEdge(3, 3); 

	cout << "Following is Breadth First Traversal "
		<< "(starting from vertex 2) \n"; 
	g.BFS(2); 

	return 0; 
} 


iii) Clone a graph

 
#include<bits/stdc++.h> 
using namespace std; 

struct GraphNode 
{ 
	int val; 

	//A neighbour vector which contains addresses to 
	//all the neighbours of a GraphNode 
	vector<GraphNode*> neighbours; 
}; 

// A function which clones a Graph and 
// returns the address to the cloned 
// src node 
GraphNode *cloneGraph(GraphNode *src) 
{ 
	//A Map to keep track of all the 
	//nodes which have already been created 
	map<GraphNode*, GraphNode*> m; 
	queue<GraphNode*> q; 

	// Enqueue src node 
	q.push(src); 
	GraphNode *node; 

	// Make a clone Node 
	node = new GraphNode(); 
	node->val = src->val; 

	// Put the clone node into the Map 
	m[src] = node; 
	while (!q.empty()) 
	{ 
		//Get the front node from the queue 
		//and then visit all its neighbours 
		GraphNode *u = q.front(); 
		q.pop(); 
		vector<GraphNode *> v = u->neighbours; 
		int n = v.size(); 
		for (int i = 0; i < n; i++) 
		{ 
			// Check if this node has already been created 
			if (m[v[i]] == NULL) 
			{ 
				// If not then create a new Node and 
				// put into the HashMap 
				node = new GraphNode(); 
				node->val = v[i]->val; 
				m[v[i]] = node; 
				q.push(v[i]); 
			} 

			// add these neighbours to the cloned graph node 
			m[u]->neighbours.push_back(m[v[i]]); 
		} 
	} 

	// Return the address of cloned src Node 
	return m[src]; 
} 

// Build the desired graph 
GraphNode *buildGraph() 
{ 
	/* 
		Note : All the edges are Undirected 
		Given Graph: 
		1--2 
		| | 
		4--3 
	*/
	GraphNode *node1 = new GraphNode(); 
	node1->val = 1; 
	GraphNode *node2 = new GraphNode(); 
	node2->val = 2; 
	GraphNode *node3 = new GraphNode(); 
	node3->val = 3; 
	GraphNode *node4 = new GraphNode(); 
	node4->val = 4; 
	vector<GraphNode *> v; 
	v.push_back(node2); 
	v.push_back(node4); 
	node1->neighbours = v; 
	v.clear(); 
	v.push_back(node1); 
	v.push_back(node3); 
	node2->neighbours = v; 
	v.clear(); 
	v.push_back(node2); 
	v.push_back(node4); 
	node3->neighbours = v; 
	v.clear(); 
	v.push_back(node3); 
	v.push_back(node1); 
	node4->neighbours = v; 
	return node1; 
} 

// A simple bfs traversal of a graph to 
// check for proper cloning of the graph 
void bfs(GraphNode *src) 
{ 
	map<GraphNode*, bool> visit; 
	queue<GraphNode*> q; 
	q.push(src); 
	visit[src] = true; 
	while (!q.empty()) 
	{ 
		GraphNode *u = q.front(); 
		cout << "Value of Node " << u->val << "\n"; 
		cout << "Address of Node " <<u << "\n"; 
		q.pop(); 
		vector<GraphNode *> v = u->neighbours; 
		int n = v.size(); 
		for (int i = 0; i < n; i++) 
		{ 
			if (!visit[v[i]]) 
			{ 
				visit[v[i]] = true; 
				q.push(v[i]); 
			} 
		} 
	} 
	cout << endl; 
} 


int main() 
{ 
	GraphNode *src = buildGraph(); 
	cout << "BFS Traversal before cloning\n"; 
	bfs(src); 
	GraphNode *newsrc = cloneGraph(src); 
	cout << "BFS Traversal after cloning\n"; 
	bfs(newsrc); 
	return 0; 
} 


iv) Cycle detection in an undirected graph


#include<iostream> 
#include <list> 
#include <limits.h> 
using namespace std; 

// Class for an undirected graph 
class Graph 
{ 
	int V; // No. of vertices 
	list<int> *adj; // Pointer to an array containing adjacency lists 
	bool isCyclicUtil(int v, bool visited[], int parent); 
public: 
	Graph(int V); // Constructor 
	void addEdge(int v, int w); // to add an edge to graph 
	bool isCyclic(); // returns true if there is a cycle 
}; 

Graph::Graph(int V) 
{ 
	this->V = V; 
	adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
	adj[v].push_back(w); // Add w to v’s list. 
	adj[w].push_back(v); // Add v to w’s list. 
} 

// A recursive function that uses visited[] and parent to detect 
// cycle in subgraph reachable from vertex v. 
bool Graph::isCyclicUtil(int v, bool visited[], int parent) 
{ 
	// Mark the current node as visited 
	visited[v] = true; 

	// Recur for all the vertices adjacent to this vertex 
	list<int>::iterator i; 
	for (i = adj[v].begin(); i != adj[v].end(); ++i) 
	{ 
		// If an adjacent is not visited, then recur for that adjacent 
		if (!visited[*i]) 
		{ 
		if (isCyclicUtil(*i, visited, v)) 
			return true; 
		} 

		// If an adjacent is visited and not parent of current vertex, 
		// then there is a cycle. 
		else if (*i != parent) 
		return true; 
	} 
	return false; 
} 

// Returns true if the graph contains a cycle, else false. 
bool Graph::isCyclic() 
{ 
	// Mark all the vertices as not visited and not part of recursion 
	// stack 
	bool *visited = new bool[V]; 
	for (int i = 0; i < V; i++) 
		visited[i] = false; 

	// Call the recursive helper function to detect cycle in different 
	// DFS trees 
	for (int u = 0; u < V; u++) 
		if (!visited[u]) // Don't recur for u if it is already visited 
		if (isCyclicUtil(u, visited, -1)) 
			return true; 

	return false; 
} 

 
int main() 
{ 
	Graph g1(5); 
	g1.addEdge(1, 0); 
	g1.addEdge(0, 2); 
	g1.addEdge(2, 1); 
	g1.addEdge(0, 3); 
	g1.addEdge(3, 4); 
	g1.isCyclic()? cout << "Graph contains cycle\n": 
				cout << "Graph doesn't contain cycle\n"; 

	Graph g2(3); 
	g2.addEdge(0, 1); 
	g2.addEdge(1, 2); 
	g2.isCyclic()? cout << "Graph contains cycle\n": 
				cout << "Graph doesn't contain cycle\n"; 

	return 0; 
} 


v) Cycle detection in a directed graph


#include<bits/stdc++.h> 

using namespace std; 

class Graph 
{ 
	int V; // No. of vertices 
	list<int> *adj; // Pointer to an array containing adjacency lists 
	bool isCyclicUtil(int v, bool visited[], bool *rs); // used by isCyclic() 
public: 
	Graph(int V); // Constructor 
	void addEdge(int v, int w); // to add an edge to graph 
	bool isCyclic(); // returns true if there is a cycle in this graph 
}; 

Graph::Graph(int V) 
{ 
	this->V = V; 
	adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
	adj[v].push_back(w); // Add w to v’s list. 
} 

// This function is a variation of DFSUtil() in https://www.geeksforgeeks.org/archives/18212 
bool Graph::isCyclicUtil(int v, bool visited[], bool *recStack) 
{ 
	if(visited[v] == false) 
	{ 
		// Mark the current node as visited and part of recursion stack 
		visited[v] = true; 
		recStack[v] = true; 

		// Recur for all the vertices adjacent to this vertex 
		list<int>::iterator i; 
		for(i = adj[v].begin(); i != adj[v].end(); ++i) 
		{ 
			if ( !visited[*i] && isCyclicUtil(*i, visited, recStack) ) 
				return true; 
			else if (recStack[*i]) 
				return true; 
		} 

	} 
	recStack[v] = false; // remove the vertex from recursion stack 
	return false; 
} 

// Returns true if the graph contains a cycle, else false. 
// This function is a variation of DFS() in https://www.geeksforgeeks.org/archives/18212 
bool Graph::isCyclic() 
{ 
	// Mark all the vertices as not visited and not part of recursion 
	// stack 
	bool *visited = new bool[V]; 
	bool *recStack = new bool[V]; 
	for(int i = 0; i < V; i++) 
	{ 
		visited[i] = false; 
		recStack[i] = false; 
	} 

	// Call the recursive helper function to detect cycle in different 
	// DFS trees 
	for(int i = 0; i < V; i++) 
		if (isCyclicUtil(i, visited, recStack)) 
			return true; 

	return false; 
} 

int main() 
{ 
	// Create a graph given in the above diagram 
	Graph g(4); 
	g.addEdge(0, 1); 
	g.addEdge(0, 2); 
	g.addEdge(1, 2); 
	g.addEdge(2, 0); 
	g.addEdge(2, 3); 
	g.addEdge(3, 3); 

	if(g.isCyclic()) 
		cout << "Graph contains cycle"; 
	else
		cout << "Graph doesn't contain cycle"; 
	return 0; 
} 


vi) Topo sort 


#include<iostream> 
#include <list> 
#include <stack> 
using namespace std; 

// Class to represent a graph 
class Graph 
{ 
// No. of vertices' 
	int V;	 

	// Pointer to an array containing adjacency listsList 
	list<int> *adj; 

	// A function used by topologicalSort 
	void topologicalSortUtil(int v, bool visited[], 
stack<int> &Stack); 
public: 
// Constructor 
	Graph(int V); 

	// function to add an edge to graph 
	void addEdge(int v, int w); 

	// prints a Topological Sort of 
// the complete graph 
	void topologicalSort(); 
}; 

Graph::Graph(int V) 
{ 
	this->V = V; 
	adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
// Add w to v’s list. 
	adj[v].push_back(w); 
} 

// A recursive function used by topologicalSort 
void Graph::topologicalSortUtil( 
int v, bool visited[], 
								stack<int> &Stack) 
{ 
	// Mark the current node as visited. 
	visited[v] = true; 

	// Recur for all the vertices 
// adjacent to this vertex 
	list<int>::iterator i; 
	for (i = adj[v].begin(); i != adj[v].end(); ++i) 
		if (!visited[*i]) 
			topologicalSortUtil(*i, visited, Stack); 

	// Push current vertex to stack 
// which stores result 
	Stack.push(v); 
} 

// The function to do Topological Sort. 
// It uses recursive topologicalSortUtil() 
void Graph::topologicalSort() 
{ 
	stack<int> Stack; 

	// Mark all the vertices as not visited 
	bool *visited = new bool[V]; 
	for (int i = 0; i < V; i++) 
		visited[i] = false; 

	// Call the recursive helper function 
// to store Topological 
	// Sort starting from all 
// vertices one by one 
	for (int i = 0; i < V; i++) 
	if (visited[i] == false) 
		topologicalSortUtil(i, visited, Stack); 

	// Print contents of stack 
	while (Stack.empty() == false) 
	{ 
		cout << Stack.top() << " "; 
		Stack.pop(); 
	} 
} 


int main() 
{ 
	// Create a graph given in the above diagram 
	Graph g(6); 
	g.addEdge(5, 2); 
	g.addEdge(5, 0); 
	g.addEdge(4, 0); 
	g.addEdge(4, 1); 
	g.addEdge(2, 3); 
	g.addEdge(3, 1); 

	cout << "Following is a Topological Sort of the given graph \n"; 
	g.topologicalSort(); 

	return 0; 
} 


vii)  


#include <bits/stdc++.h> 
using namespace std; 

#define ROW 5 
#define COL 5 

// A function to check if a given 
// cell (row, col) can be included in DFS 
int isSafe(int M[][COL], int row, int col, 
		bool visited[][COL]) 
{ 
	// row number is in range, column 
	// number is in range and value is 1 
	// and not yet visited 
	return (row >= 0) && (row < ROW) && (col >= 0) && (col < COL) && (M[row][col] && !visited[row][col]); 
} 

// A utility function to do DFS for a 
// 2D boolean matrix. It only considers 
// the 8 neighbours as adjacent vertices 
void DFS(int M[][COL], int row, int col, 
		bool visited[][COL]) 
{ 
	// These arrays are used to get 
	// row and column numbers of 8 
	// neighbours of a given cell 
	static int rowNbr[] = { -1, -1, -1, 0, 0, 1, 1, 1 }; 
	static int colNbr[] = { -1, 0, 1, -1, 1, -1, 0, 1 }; 

	// Mark this cell as visited 
	visited[row][col] = true; 

	// Recur for all connected neighbours 
	for (int k = 0; k < 8; ++k) 
		if (isSafe(M, row + rowNbr[k], col + colNbr[k], visited)) 
			DFS(M, row + rowNbr[k], col + colNbr[k], visited); 
} 

// The main function that returns 
// count of islands in a given boolean 
// 2D matrix 
int countIslands(int M[][COL]) 
{ 
	// Make a bool array to mark visited cells. 
	// Initially all cells are unvisited 
	bool visited[ROW][COL]; 
	memset(visited, 0, sizeof(visited)); 

	// Initialize count as 0 and 
	// travese through the all cells of 
	// given matrix 
	int count = 0; 
	for (int i = 0; i < ROW; ++i) 
		for (int j = 0; j < COL; ++j) 

			// If a cell with value 1 is not 
			if (M[i][j] && !visited[i][j]) { 
				// visited yet, then new island found 
				// Visit all cells in this island. 
				DFS(M, i, j, visited); 

				// and increment island count 
				++count; 
			} 

	return count; 
} 

 
int main() 
{ 
	int M[][COL] = { { 1, 1, 0, 0, 0 }, 
					{ 0, 1, 0, 0, 1 }, 
					{ 1, 0, 0, 1, 1 }, 
					{ 0, 0, 0, 0, 0 }, 
					{ 1, 0, 1, 0, 1 } }; 

	cout << "Number of islands is: " << countIslands(M); 

	return 0; 
} 


viii) Bipartite check


#include <bits/stdc++.h> 

using namespace std; 

const int V = 4; 

// This function returns true if 
// graph G[V][V] is Bipartite, else false 
bool isBipartiteUtil(int G[][V], int src, int colorArr[]) 
{ 
	colorArr[src] = 1; 

	// Create a queue (FIFO) of vertex numbers a 
	// nd enqueue source vertex for BFS traversal 
	queue <int> q; 
	q.push(src); 

	// Run while there are vertices in queue (Similar to BFS) 
	while (!q.empty()) 
	{ 
		// Dequeue a vertex from queue ( Refer http://goo.gl/35oz8 ) 
		int u = q.front(); 
		q.pop(); 

		// Return false if there is a self-loop 
		if (G[u][u] == 1) 
		return false; 

		// Find all non-colored adjacent vertices 
		for (int v = 0; v < V; ++v) 
		{ 
			// An edge from u to v exists and 
			// destination v is not colored 
			if (G[u][v] && colorArr[v] == -1) 
			{ 
				// Assign alternate color to this 
				// adjacent v of u 
				colorArr[v] = 1 - colorArr[u]; 
				q.push(v); 
			} 

			// An edge from u to v exists and destination 
			// v is colored with same color as u 
			else if (G[u][v] && colorArr[v] == colorArr[u]) 
				return false; 
		} 
	} 

	// If we reach here, then all adjacent vertices can 
	// be colored with alternate color 
	return true; 
} 

// Returns true if G[][] is Bipartite, else false 
bool isBipartite(int G[][V]) 
{ 
	// Create a color array to store colors assigned to all 
	// veritces. Vertex/ number is used as index in this 
	// array. The value '-1' of colorArr[i] is used to 
	// ndicate that no color is assigned to vertex 'i'. 
	// The value 1 is used to indicate first color is 
	// assigned and value 0 indicates second color is 
	// assigned. 
	int colorArr[V]; 
	for (int i = 0; i < V; ++i) 
		colorArr[i] = -1; 

	// This code is to handle disconnected graoh 
	for (int i = 0; i < V; i++) 
	if (colorArr[i] == -1) 
		if (isBipartiteUtil(G, i, colorArr) == false) 
		return false; 

	return true; 
} 


int main() 
{ 
	int G[][V] = {{0, 1, 0, 1}, 
		{1, 0, 1, 0}, 
		{0, 1, 0, 1}, 
		{1, 0, 1, 0} 
	}; 

	isBipartite(G) ? cout << "Yes" : cout << "No"; 
	return 0; 
} 












 












