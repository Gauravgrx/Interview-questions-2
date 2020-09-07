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



 












