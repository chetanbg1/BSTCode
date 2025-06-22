# BSTCode
1. Create a Binary Tree Node class

java
Copy
Edit
class Node {
    int data;
    Node left, right;

    Node(int item) {
        data = item;
        left = right = null;
    }
}
2. Insert node in Binary Search Tree (BST)

java
Copy
Edit
class BST {
    Node root;

    Node insert(Node root, int data) {
        if (root == null) return new Node(data);
        if (data < root.data) root.left = insert(root.left, data);
        else if (data > root.data) root.right = insert(root.right, data);
        return root;
    }

    public static void main(String[] args) {
        BST tree = new BST();
        tree.root = tree.insert(tree.root, 10);
        tree.root = tree.insert(tree.root, 5);
        tree.root = tree.insert(tree.root, 15);
    }
}
3. Inorder Traversal of Binary Tree

java
Copy
Edit
void inorder(Node root) {
    if (root != null) {
        inorder(root.left);
        System.out.print(root.data + " ");
        inorder(root.right);
    }
}
4. Preorder Traversal of Binary Tree

java
Copy
Edit
void preorder(Node root) {
    if (root != null) {
        System.out.print(root.data + " ");
        preorder(root.left);
        preorder(root.right);
    }
}
5. Postorder Traversal of Binary Tree

java
Copy
Edit
void postorder(Node root) {
    if (root != null) {
        postorder(root.left);
        postorder(root.right);
        System.out.print(root.data + " ");
    }
}
6. Search for a value in BST

java
Copy
Edit
boolean search(Node root, int key) {
    if (root == null) return false;
    if (root.data == key) return true;
    if (key < root.data) return search(root.left, key);
    else return search(root.right, key);
}
7. Find minimum value node in BST

java
Copy
Edit
Node minValueNode(Node root) {
    Node current = root;
    while (current.left != null) current = current.left;
    return current;
}
8. Delete a node in BST

java
Copy
Edit
Node deleteNode(Node root, int key) {
    if (root == null) return root;
    if (key < root.data) root.left = deleteNode(root.left, key);
    else if (key > root.data) root.right = deleteNode(root.right, key);
    else {
        // node with one or no child
        if (root.left == null) return root.right;
        else if (root.right == null) return root.left;
        // node with two children
        Node temp = minValueNode(root.right);
        root.data = temp.data;
        root.right = deleteNode(root.right, temp.data);
    }
    return root;
}
9. Find height of binary tree

java
Copy
Edit
int height(Node root) {
    if (root == null) return 0;
    return 1 + Math.max(height(root.left), height(root.right));
}
10. Level order traversal (BFS) of binary tree

java
Copy
Edit
void levelOrder(Node root) {
    if (root == null) return;
    Queue<Node> queue = new LinkedList<>();
    queue.add(root);
    while (!queue.isEmpty()) {
        Node temp = queue.poll();
        System.out.print(temp.data + " ");
        if (temp.left != null) queue.add(temp.left);
        if (temp.right != null) queue.add(temp.right);
    }
}
10. Count total nodes in a binary tree

java
Copy
Edit
int countNodes(Node root) {
    if (root == null) return 0;
    return 1 + countNodes(root.left) + countNodes(root.right);
}
11. Count leaf nodes in a binary tree

java
Copy
Edit
int countLeaves(Node root) {
    if (root == null) return 0;
    if (root.left == null && root.right == null) return 1;
    return countLeaves(root.left) + countLeaves(root.right);
}
12. Check if binary tree is a BST

java
Copy
Edit
boolean isBST(Node root) {
    return isBSTUtil(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
}

boolean isBSTUtil(Node node, int min, int max) {
    if (node == null) return true;
    if (node.data < min || node.data > max) return false;
    return isBSTUtil(node.left, min, node.data - 1) &&
           isBSTUtil(node.right, node.data + 1, max);
}
13. Mirror of a binary tree

java
Copy
Edit
Node mirror(Node root) {
    if (root == null) return null;
    Node left = mirror(root.left);
    Node right = mirror(root.right);
    root.left = right;
    root.right = left;
    return root;
}
14. Check if two binary trees are identical

java
Copy
Edit
boolean isIdentical(Node root1, Node root2) {
    if (root1 == null && root2 == null) return true;
    if (root1 == null || root2 == null) return false;
    return (root1.data == root2.data) &&
           isIdentical(root1.left, root2.left) &&
           isIdentical(root1.right, root2.right);
}
15. Find maximum value in a binary tree

java
Copy
Edit
int findMax(Node root) {
    if (root == null) return Integer.MIN_VALUE;
    return Math.max(root.data, Math.max(findMax(root.left), findMax(root.right)));
}
16. Find minimum value in a binary tree

java
Copy
Edit
int findMin(Node root) {
    if (root == null) return Integer.MAX_VALUE;
    return Math.min(root.data, Math.min(findMin(root.left), findMin(root.right)));
}
17. Print all root to leaf paths

java
Copy
Edit
void printPaths(Node root) {
    int[] path = new int[1000];
    printPathsRec(root, path, 0);
}

void printPathsRec(Node node, int[] path, int pathLen) {
    if (node == null) return;
    path[pathLen] = node.data;
    pathLen++;
    if (node.left == null && node.right == null) printArray(path, pathLen);
    else {
        printPathsRec(node.left, path, pathLen);
        printPathsRec(node.right, path, pathLen);
    }
}

void printArray(int[] ints, int len) {
    for (int i = 0; i < len; i++) {
        System.out.print(ints[i] + " ");
    }
    System.out.println();
}
18. Calculate diameter of binary tree

java
Copy
Edit
int diameter(Node root) {
    if (root == null) return 0;
    int leftHeight = height(root.left);
    int rightHeight = height(root.right);

    int leftDiameter = diameter(root.left);
    int rightDiameter = diameter(root.right);

    return Math.max(leftHeight + rightHeight + 1, Math.max(leftDiameter, rightDiameter));
}
19. Find Lowest Common Ancestor (LCA) in BST

java
Copy
Edit
Node lca(Node root, int n1, int n2) {
    if (root == null) return null;

    if (root.data > n1 && root.data > n2) return lca(root.left, n1, n2);
    if (root.data < n1 && root.data < n2) return lca(root.right, n1, n2);

    return root;
}
20. Convert sorted array to Balanced BST

java
Copy
Edit
Node sortedArrayToBST(int[] arr, int start, int end) {
    if (start > end) return null;

    int mid = (start + end) / 2;
    Node root = new Node(arr[mid]);

    root.left = sortedArrayToBST(arr, start, mid - 1);
    root.right = sortedArrayToBST(arr, mid + 1, end);

    return root;
}
21. Convert BST to sorted doubly linked list (in-place)

java
Copy
Edit
Node prev = null;
Node headDLL = null;

void bstToDLL(Node root) {
    if (root == null) return;

    bstToDLL(root.left);

    if (prev == null) {
        headDLL = root;
    } else {
        root.left = prev;
        prev.right = root;
    }
    prev = root;

    bstToDLL(root.right);
}
22. Check if a binary tree is height-balanced

java
Copy
Edit
boolean isBalanced(Node root) {
    return checkHeight(root) != -1;
}

int checkHeight(Node node) {
    if (node == null) return 0;

    int lh = checkHeight(node.left);
    if (lh == -1) return -1;

    int rh = checkHeight(node.right);
    if (rh == -1) return -1;

    if (Math.abs(lh - rh) > 1) return -1;

    return 1 + Math.max(lh, rh);
}
23. Right view of binary tree

java
Copy
Edit
void rightView(Node root) {
    rightViewUtil(root, 0, new int[]{-1});
}

void rightViewUtil(Node node, int level, int[] maxLevel) {
    if (node == null) return;

    if (level > maxLevel[0]) {
        System.out.print(node.data + " ");
        maxLevel[0] = level;
    }

    rightViewUtil(node.right, level + 1, maxLevel);
    rightViewUtil(node.left, level + 1, maxLevel);
}
24. Left view of binary tree

java
Copy
Edit
void leftView(Node root) {
    leftViewUtil(root, 0, new int[]{-1});
}

void leftViewUtil(Node node, int level, int[] maxLevel) {
    if (node == null) return;

    if (level > maxLevel[0]) {
        System.out.print(node.data + " ");
        maxLevel[0] = level;
    }

    leftViewUtil(node.left, level + 1, maxLevel);
    leftViewUtil(node.right, level + 1, maxLevel);
}
25. Zigzag (spiral) level order traversal

java
Copy
Edit
void zigzagTraversal(Node root) {
    if (root == null) return;

    Stack<Node> currLevel = new Stack<>();
    Stack<Node> nextLevel = new Stack<>();
    boolean leftToRight = true;

    currLevel.push(root);

    while (!currLevel.isEmpty()) {
        Node node = currLevel.pop();
        System.out.print(node.data + " ");

        if (leftToRight) {
            if (node.left != null) nextLevel.push(node.left);
            if (node.right != null) nextLevel.push(node.right);
        } else {
            if (node.right != null) nextLevel.push(node.right);
            if (node.left != null) nextLevel.push(node.left);
        }

        if (currLevel.isEmpty()) {
            leftToRight = !leftToRight;
            Stack<Node> temp = currLevel;
            currLevel = nextLevel;
            nextLevel = temp;
        }
    }
}
26. Print all ancestors of a given node

java
Copy
Edit
boolean printAncestors(Node root, int target) {
    if (root == null) return false;

    if (root.data == target) return true;

    if (printAncestors(root.left, target) || printAncestors(root.right, target)) {
        System.out.print(root.data + " ");
        return true;
    }
    return false;
}
27. Sum of all nodes in binary tree

java
Copy
Edit
int sumOfNodes(Node root) {
    if (root == null) return 0;
    return root.data + sumOfNodes(root.left) + sumOfNodes(root.right);
}
28. Find distance between two nodes in BST

java
Copy
Edit
int distanceBetweenNodes(Node root, int a, int b) {
    Node lca = lca(root, a, b);
    return distanceFromLCA(lca, a) + distanceFromLCA(lca, b);
}

int distanceFromLCA(Node root, int val) {
    if (root == null) return 0;
    if (root.data == val) return 0;
    if (val < root.data) return 1 + distanceFromLCA(root.left, val);
    else return 1 + distanceFromLCA(root.right, val);
}
29. Sum of leaf nodes


int sumLeafNodes(Node root) {
    if (root == null) return 0;
    if (root.left == null && root.right == null) return root.data;
    return sumLeafNodes(root.left) + sumLeafNodes(root.right);
}
30. Count non-leaf (internal) nodes

java
Copy
Edit
int countInternalNodes(Node root) {
    if (root == null || (root.left == null && root.right == null)) return 0;
    return 1 + countInternalNodes(root.left) + countInternalNodes(root.right);
}
31. Print nodes at a given level

java
Copy
Edit
void printLevel(Node root, int level) {
    if (root == null) return;
    if (level == 1) System.out.print(root.data + " ");
    else {
        printLevel(root.left, level - 1);
        printLevel(root.right, level - 1);
    }
}
32. Find depth of a node in binary tree

java
Copy
Edit
int findDepth(Node root, int key, int level) {
    if (root == null) return -1;
    if (root.data == key) return level;

    int left = findDepth(root.left, key, level + 1);
    if (left != -1) return left;

    return findDepth(root.right, key, level + 1);
}
33. Convert Binary Tree to Doubly Linked List (in-order)

java
Copy
Edit
class Converter {
    Node head = null, prev = null;

    void convertToDLL(Node root) {
        if (root == null) return;

        convertToDLL(root.left);

        if (prev == null) head = root;
        else {
            prev.right = root;
            root.left = prev;
        }
        prev = root;

        convertToDLL(root.right);
    }
}
34. Print all nodes at distance K from root

java
Copy
Edit
void printKDistance(Node root, int k) {
    if (root == null) return;
    if (k == 0) {
        System.out.print(root.data + " ");
        return;
    }
    printKDistance(root.left, k - 1);
    printKDistance(root.right, k - 1);
}
35. Check if a given node exists in Binary Tree

java
Copy
Edit
boolean exists(Node root, int key) {
    if (root == null) return false;
    if (root.data == key) return true;
    return exists(root.left, key) || exists(root.right, key);
}
36. Find maximum width of binary tree

java
Copy
Edit
int getMaxWidth(Node root) {
    if (root == null) return 0;
    Queue<Node> q = new LinkedList<>();
    q.add(root);
    int maxWidth = 0;

    while (!q.isEmpty()) {
        int count = q.size();
        maxWidth = Math.max(maxWidth, count);

        for (int i = 0; i < count; i++) {
            Node temp = q.poll();
            if (temp.left != null) q.add(temp.left);
            if (temp.right != null) q.add(temp.right);
        }
    }
    return maxWidth;
}
37. Convert Binary Tree to its Mirror Tree (iterative)

java
Copy
Edit
void mirrorIterative(Node root) {
    if (root == null) return;

    Queue<Node> q = new LinkedList<>();
    q.add(root);

    while (!q.isEmpty()) {
        Node curr = q.poll();
        Node temp = curr.left;
        curr.left = curr.right;
        curr.right = temp;

        if (curr.left != null) q.add(curr.left);
        if (curr.right != null) q.add(curr.right);
    }
}
38. Print path from root to given node

java
Copy
Edit
boolean getPath(Node root, int target, List<Integer> path) {
    if (root == null) return false;
    path.add(root.data);
    if (root.data == target) return true;

    if (getPath(root.left, target, path) || getPath(root.right, target, path)) return true;

    path.remove(path.size() - 1);
    return false;
}
39. Print all nodes between two levels


void printBetweenLevels(Node root, int low, int high) {
    if (root == null) return;

    Queue<Node> q = new LinkedList<>();
    q.add(root);
    int level = 0;

    while (!q.isEmpty()) {
        int size = q.size();
        level++;

        for (int i = 0; i < size; i++) {
            Node node = q.poll();
            if (level >= low && level <= high) System.out.print(node.data + " ");
            if (node.left != null) q.add(node.left);
            if (node.right != null) q.add(node.right);
        }
    }
}
Program 40: Check if a binary tree is symmetric (mirror of itself)
java
Copy
Edit
class SymmetricTree {

    static class Node {
        int data;
        Node left, right;
        Node(int val) {
            data = val;
        }
    }

    static boolean isSymmetric(Node root) {
        return root == null || isMirror(root.left, root.right);
    }

    static boolean isMirror(Node t1, Node t2) {
        if (t1 == null && t2 == null) return true;
        if (t1 == null || t2 == null) return false;

        return (t1.data == t2.data)
                && isMirror(t1.left, t2.right)
                && isMirror(t1.right, t2.left);
    }

    public static void main(String[] args) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(2);
        root.left.left = new Node(3);
        root.left.right = new Node(4);
        root.right.left = new Node(4);
        root.right.right = new Node(3);

        System.out.println("Is Symmetric: " + isSymmetric(root));
    }
}
✅ Program 41: Print all nodes with no sibling
java
Copy
Edit
class NoSiblings {

    static class Node {
        int data;
        Node left, right;
        Node(int val) {
            data = val;
        }
    }

    static void printNodesWithNoSiblings(Node root) {
        if (root == null) return;

        if (root.left != null && root.right == null)
            System.out.print(root.left.data + " ");
        if (root.right != null && root.left == null)
            System.out.print(root.right.data + " ");

        printNodesWithNoSiblings(root.left);
        printNodesWithNoSiblings(root.right);
    }

    public static void main(String[] args) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.left.left = new Node(4);
        root.right = new Node(3);
        root.right.right = new Node(5);

        printNodesWithNoSiblings(root);
    }
}
✅ Program 42: Find node level in binary tree
java
Copy
Edit
class NodeLevel {

    static class Node {
        int data;
        Node left, right;
        Node(int val) {
            data = val;
        }
    }

    static int getLevel(Node root, int key, int level) {
        if (root == null) return 0;
        if (root.data == key) return level;

        int downlevel = getLevel(root.left, key, level + 1);
        if (downlevel != 0) return downlevel;

        return getLevel(root.right, key, level + 1);
    }

    public static void main(String[] args) {
        Node root = new Node(3);
        root.left = new Node(2);
        root.right = new Node(5);
        root.right.left = new Node(4);

        int key = 4;
        System.out.println("Level of " + key + ": " + getLevel(root, key, 1));
    }
}
✅ Program 43: Count number of full nodes (both left and right child)
java
Copy
Edit
class FullNodes {

    static class Node {
        int data;
        Node left, right;
        Node(int val) {
            data = val;
        }
    }

    static int countFullNodes(Node root) {
        if (root == null) return 0;
        int count = countFullNodes(root.left) + countFullNodes(root.right);
        if (root.left != null && root.right != null) count++;
        return count;
    }

    public static void main(String[] args) {
        Node root = new Node(10);
        root.left = new Node(20);
        root.right = new Node(30);
        root.left.left = new Node(40);
        root.left.right = new Node(50);

        System.out.println("Full nodes: " + countFullNodes(root));
    }
}
✅ Program 44: Check if a path exists for a sum (root-to-leaf)
java
Copy
Edit
class PathSum {

    static class Node {
        int data;
        Node left, right;
        Node(int val) {
            data = val;
        }
    }

    static boolean hasPathSum(Node root, int sum) {
        if (root == null) return false;

        if (root.left == null && root.right == null && root.data == sum)
            return true;

        return hasPathSum(root.left, sum - root.data) ||
               hasPathSum(root.right, sum - root.data);
    }

    public static void main(String[] args) {
        Node root = new Node(5);
        root.left = new Node(4);
        root.right = new Node(8);
        root.left.left = new Node(11);
        root.left.left.left = new Node(7);
        root.left.left.right = new Node(2);

        int sum = 22;
        System.out.println("Has path sum: " + hasPathSum(root, sum));
    }
}
✅ Program 45: Count all paths with a given sum (not necessarily root-to-leaf)
java
Copy
Edit
class CountPathsSum {

    static class Node {
        int data;
        Node left, right;
        Node(int val) {
            data = val;
        }
    }

    static int countPaths(Node root, int sum) {
        if (root == null) return 0;
        return countFromNode(root, sum) +
               countPaths(root.left, sum) +
               countPaths(root.right, sum);
    }

    static int countFromNode(Node node, int sum) {
        if (node == null) return 0;
        int count = 0;
        if (node.data == sum) count++;
        count += countFromNode(node.left, sum - node.data);
        count += countFromNode(node.right, sum - node.data);
        return count;
    }

    public static void main(String[] args) {
        Node root = new Node(10);
        root.left = new Node(5);
        root.right = new Node(-3);
        root.left.left = new Node(3);
        root.left.right = new Node(2);
        root.left.left.left = new Node(3);
        root.left.left.right = new Node(-2);
        root.left.right.right = new Node(1);
        root.right.right = new Node(11);

        System.out.println("Paths with sum 8: " + countPaths(root, 8));
    }
}
✅ Program 46: Print boundary nodes of binary tree (anticlockwise)
java
Copy
Edit
class BoundaryTraversal {

    static class Node {
        int data;
        Node left, right;
        Node(int val) {
            data = val;
        }
    }

    static void printBoundary(Node root) {
        if (root == null) return;
        System.out.print(root.data + " ");
        printLeftBoundary(root.left);
        printLeaves(root.left);
        printLeaves(root.right);
        printRightBoundary(root.right);
    }

    static void printLeftBoundary(Node node) {
        if (node == null) return;
        if (node.left != null) {
            System.out.print(node.data + " ");
            printLeftBoundary(node.left);
        } else if (node.right != null) {
            System.out.print(node.data + " ");
            printLeftBoundary(node.right);
        }
    }

    static void printRightBoundary(Node node) {
        if (node == null) return;
        if (node.right != null) {
            printRightBoundary(node.right);
            System.out.print(node.data + " ");
        } else if (node.left != null) {
            printRightBoundary(node.left);
            System.out.print(node.data + " ");
        }
    }

    static void printLeaves(Node node) {
        if (node == null) return;
        printLeaves(node.left);
        if (node.left == null && node.right == null)
            System.out.print(node.data + " ");
        printLeaves(node.right);
    }

    public static void main(String[] args) {
        Node root = new Node(20);
        root.left = new Node(8);
        root.left.left = new Node(4);
        root.left.right = new Node(12);
        root.left.right.left = new Node(10);
        root.left.right.right = new Node(14);
        root.right = new Node(22);
        root.right.right = new Node(25);

        printBoundary(root);
    }
}
Program 47: Check if two trees are mirror of each other
java
Copy
Edit
class MirrorTrees {

    static class Node {
        int data;
        Node left, right;
        Node(int val) {
            data = val;
        }
    }

    static boolean areMirror(Node a, Node b) {
        if (a == null && b == null) return true;
        if (a == null || b == null) return false;
        return (a.data == b.data)
                && areMirror(a.left, b.right)
                && areMirror(a.right, b.left);
    }

    public static void main(String[] args) {
        Node a = new Node(1);
        a.left = new Node(2);
        a.right = new Node(3);

        Node b = new Node(1);
        b.left = new Node(3);
        b.right = new Node(2);

        System.out.println("Are Mirror: " + areMirror(a, b));
    }
}
✅ Program 48: Find diameter using single traversal (optimized)
java
Copy
Edit
class DiameterOptimized {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static class TreeInfo {
        int height;
        int diameter;

        TreeInfo(int height, int diameter) {
            this.height = height;
            this.diameter = diameter;
        }
    }

    static TreeInfo diameter(Node root) {
        if (root == null) return new TreeInfo(0, 0);

        TreeInfo left = diameter(root.left);
        TreeInfo right = diameter(root.right);

        int height = 1 + Math.max(left.height, right.height);
        int dia = Math.max(left.height + right.height + 1,
                          Math.max(left.diameter, right.diameter));

        return new TreeInfo(height, dia);
    }

    public static void main(String[] args) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);

        System.out.println("Diameter: " + diameter(root).diameter);
    }
}
✅ Program 49: Create tree from inorder and preorder traversals
java
Copy
Edit
import java.util.*;

class BuildTreeInPre {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static int preIndex = 0;

    static Node buildTree(int[] in, int[] pre, int inStart, int inEnd, Map<Integer, Integer> inMap) {
        if (inStart > inEnd) return null;

        int curr = pre[preIndex++];
        Node node = new Node(curr);
        int inIndex = inMap.get(curr);

        node.left = buildTree(in, pre, inStart, inIndex - 1, inMap);
        node.right = buildTree(in, pre, inIndex + 1, inEnd, inMap);
        return node;
    }

    static void printInorder(Node root) {
        if (root == null) return;
        printInorder(root.left);
        System.out.print(root.data + " ");
        printInorder(root.right);
    }

    public static void main(String[] args) {
        int[] inorder = {4, 2, 5, 1, 3};
        int[] preorder = {1, 2, 4, 5, 3};

        Map<Integer, Integer> inMap = new HashMap<>();
        for (int i = 0; i < inorder.length; i++)
            inMap.put(inorder[i], i);

        Node root = buildTree(inorder, preorder, 0, inorder.length - 1, inMap);
        printInorder(root);
    }
}
✅ Program 50: Check if two BSTs are equal in structure and data
java
Copy
Edit
class CompareBSTs {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static boolean areIdentical(Node a, Node b) {
        if (a == null && b == null) return true;
        if (a == null || b == null) return false;
        return (a.data == b.data)
                && areIdentical(a.left, b.left)
                && areIdentical(a.right, b.right);
    }

    public static void main(String[] args) {
        Node root1 = new Node(10);
        root1.left = new Node(5);
        root1.right = new Node(15);

        Node root2 = new Node(10);
        root2.left = new Node(5);
        root2.right = new Node(15);

        System.out.println("Identical: " + areIdentical(root1, root2));
    }
}
✅ Program 51: Convert Binary Tree to Sum Tree
java
Copy
Edit
class SumTree {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static int toSumTree(Node node) {
        if (node == null) return 0;

        int old_val = node.data;
        node.data = toSumTree(node.left) + toSumTree(node.right);

        return node.data + old_val;
    }

    static void inorder(Node root) {
        if (root == null) return;
        inorder(root.left);
        System.out.print(root.data + " ");
        inorder(root.right);
    }

    public static void main(String[] args) {
        Node root = new Node(10);
        root.left = new Node(-2);
        root.right = new Node(6);
        root.left.left = new Node(8);
        root.left.right = new Node(-4);
        root.right.left = new Node(7);
        root.right.right = new Node(5);

        toSumTree(root);
        inorder(root);
    }
}
✅ Program 52: Find minimum depth of binary tree
java
Copy
Edit
class MinDepth {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static int minDepth(Node root) {
        if (root == null) return 0;
        if (root.left == null) return 1 + minDepth(root.right);
        if (root.right == null) return 1 + minDepth(root.left);

        return 1 + Math.min(minDepth(root.left), minDepth(root.right));
    }

    public static void main(String[] args) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);

        System.out.println("Min Depth: " + minDepth(root));
    }
}
✅ Program 53: Check if tree is subtree of another tree
java
Copy
Edit
class SubtreeCheck {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static boolean isSubtree(Node root, Node subRoot) {
        if (subRoot == null) return true;
        if (root == null) return false;

        if (areIdentical(root, subRoot)) return true;

        return isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot);
    }

    static boolean areIdentical(Node a, Node b) {
        if (a == null && b == null) return true;
        if (a == null || b == null) return false;
        return (a.data == b.data) &&
               areIdentical(a.left, b.left) &&
               areIdentical(a.right, b.right);
    }

    public static void main(String[] args) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);

        Node sub = new Node(2);
        sub.left = new Node(4);

        System.out.println("Is Subtree: " + isSubtree(root, sub));
    }
}
✅ Program 54: Invert Binary Tree (mirror)
java
Copy
Edit
class InvertTree {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static Node invert(Node root) {
        if (root == null) return null;

        Node left = invert(root.left);
        Node right = invert(root.right);

        root.left = right;
        root.right = left;

        return root;
    }

    static void inorder(Node root) {
        if (root == null) return;
        inorder(root.left);
        System.out.print(root.data + " ");
        inorder(root.right);
    }

    public static void main(String[] args) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);

        invert(root);
        inorder(root);
    }
}
Program 55: Count nodes with exactly one child
java
Copy
Edit
class OneChildNodes {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static int countOneChild(Node root) {
        if (root == null) return 0;

        int count = countOneChild(root.left) + countOneChild(root.right);
        if ((root.left == null && root.right != null) ||
            (root.left != null && root.right == null))
            count++;
        return count;
    }

    public static void main(String[] args) {
        Node root = new Node(10);
        root.left = new Node(5);
        root.left.left = new Node(3);
        root.right = new Node(15);

        System.out.println("Nodes with one child: " + countOneChild(root));
    }
}
✅ Program 56: Check if Binary Tree is complete
java
Copy
Edit
import java.util.*;

class CompleteTree {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static boolean isComplete(Node root) {
        if (root == null) return true;

        Queue<Node> q = new LinkedList<>();
        q.add(root);
        boolean end = false;

        while (!q.isEmpty()) {
            Node node = q.poll();

            if (node.left != null) {
                if (end) return false;
                q.add(node.left);
            } else {
                end = true;
            }

            if (node.right != null) {
                if (end) return false;
                q.add(node.right);
            } else {
                end = true;
            }
        }

        return true;
    }

    public static void main(String[] args) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);

        System.out.println("Is complete: " + isComplete(root));
    }
}
Program 57: Find maximum node value in Binary Tree
java
Copy
Edit
class MaxInBinaryTree {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static int findMax(Node root) {
        if (root == null) return Integer.MIN_VALUE;
        int left = findMax(root.left);
        int right = findMax(root.right);
        return Math.max(root.data, Math.max(left, right));
    }

    public static void main(String[] args) {
        Node root = new Node(15);
        root.left = new Node(10);
        root.right = new Node(20);
        root.right.left = new Node(5);

        System.out.println("Maximum value: " + findMax(root));
    }
}
✅ Program 58: Find Lowest Common Ancestor (LCA) in BST
java
Copy
Edit
class LCAinBST {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static Node findLCA(Node root, int n1, int n2) {
        if (root == null) return null;

        if (n1 < root.data && n2 < root.data)
            return findLCA(root.left, n1, n2);
        else if (n1 > root.data && n2 > root.data)
            return findLCA(root.right, n1, n2);
        else
            return root;
    }

    public static void main(String[] args) {
        Node root = new Node(20);
        root.left = new Node(10);
        root.right = new Node(30);
        root.left.left = new Node(5);
        root.left.right = new Node(15);

        Node lca = findLCA(root, 5, 15);
        System.out.println("LCA: " + (lca != null ? lca.data : "Not found"));
    }
}
✅ Program 59: Delete all leaf nodes from Binary Tree
java
Copy
Edit
class DeleteLeaves {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static Node deleteLeaves(Node root) {
        if (root == null) return null;
        if (root.left == null && root.right == null)
            return null;

        root.left = deleteLeaves(root.left);
        root.right = deleteLeaves(root.right);
        return root;
    }

    static void inorder(Node root) {
        if (root == null) return;
        inorder(root.left);
        System.out.print(root.data + " ");
        inorder(root.right);
    }

    public static void main(String[] args) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);

        root = deleteLeaves(root);
        inorder(root);
    }
}
✅ Program 60: Check if Binary Tree is Height Balanced
java
Copy
Edit
class BalancedTree {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static class Height {
        int height = 0;
    }

    static boolean isBalanced(Node root, Height h) {
        if (root == null) return true;

        Height lh = new Height();
        Height rh = new Height();

        boolean left = isBalanced(root.left, lh);
        boolean right = isBalanced(root.right, rh);

        h.height = Math.max(lh.height, rh.height) + 1;

        return left && right && Math.abs(lh.height - rh.height) <= 1;
    }

    public static void main(String[] args) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.left.left = new Node(3);

        System.out.println("Is Balanced: " + isBalanced(root, new Height()));
    }
}
✅ Program 61: Count nodes greater than a given value in BST
java
Copy
Edit
class CountGreaterInBST {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static int countGreater(Node root, int x) {
        if (root == null) return 0;
        if (root.data <= x)
            return countGreater(root.right, x);
        return 1 + countGreater(root.left, x) + countGreater(root.right, x);
    }

    public static void main(String[] args) {
        Node root = new Node(15);
        root.left = new Node(10);
        root.right = new Node(20);
        root.right.right = new Node(25);

        System.out.println("Count > 15: " + countGreater(root, 15));
    }
}
✅ Program 62: Flatten Binary Tree to Linked List (Pre-order)
java
Copy
Edit
class FlattenTree {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static Node prev = null;

    static void flatten(Node root) {
        if (root == null) return;

        flatten(root.right);
        flatten(root.left);

        root.right = prev;
        root.left = null;
        prev = root;
    }

    static void printRight(Node root) {
        while (root != null) {
            System.out.print(root.data + " ");
            root = root.right;
        }
    }

    public static void main(String[] args) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(5);
        root.left.left = new Node(3);
        root.left.right = new Node(4);

        flatten(root);
        printRight(root);
    }
}
✅ Program 63: Print all root-to-leaf paths
java
Copy
Edit
import java.util.*;

class PrintAllPaths {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static void printPaths(Node root, List<Integer> path) {
        if (root == null) return;

        path.add(root.data);
        if (root.left == null && root.right == null)
            System.out.println(path);
        else {
            printPaths(root.left, path);
            printPaths(root.right, path);
        }
        path.remove(path.size() - 1);
    }

    public static void main(String[] args) {
        Node root = new Node(10);
        root.left = new Node(8);
        root.right = new Node(2);
        root.left.left = new Node(3);
        root.right.right = new Node(5);

        printPaths(root, new ArrayList<>());
    }
}
✅ Program 64: Convert Sorted Array to Balanced BST
java
Copy
Edit
class SortedArrayToBST {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static Node convert(int[] arr, int start, int end) {
        if (start > end) return null;

        int mid = (start + end) / 2;
        Node node = new Node(arr[mid]);

        node.left = convert(arr, start, mid - 1);
        node.right = convert(arr, mid + 1, end);

        return node;
    }

    static void inorder(Node root) {
        if (root == null) return;
        inorder(root.left);
        System.out.print(root.data + " ");
        inorder(root.right);
    }

    public static void main(String[] args) {
        int[] arr = {-10, -3, 0, 5, 9};
        Node root = convert(arr, 0, arr.length - 1);
        inorder(root);
    }
}
✅ Program 65: Find K-th smallest element in BST
java
Copy
Edit
class KthSmallest {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static int count = 0;

    static int kthSmallest(Node root, int k) {
        if (root == null) return -1;

        int left = kthSmallest(root.left, k);
        if (left != -1) return left;

        count++;
        if (count == k) return root.data;

        return kthSmallest(root.right, k);
    }

    public static void main(String[] args) {
        Node root = new Node(20);
        root.left = new Node(10);
        root.right = new Node(30);
        root.left.left = new Node(5);

        System.out.println("3rd Smallest: " + kthSmallest(root, 3));
    }
}
Program 66: Convert Binary Tree to String (Preorder Serialization)
java
Copy
Edit
class TreeToString {

    static class Node {
        int data;
        Node left, right;
        Node(int val) { data = val; }
    }

    static String tree2str(Node root) {
        if (root == null) return "";
        String result = root.data + "";

        if (root.left != null || root.right != null)
            result += "(" + tree2str(root.left) + ")";
        if (root.right != null)
            result += "(" + tree2str(root.right) + ")";

        return result;
    }

    public static void main(String[] args) {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.right = new Node(4);

        System.out.println(tree2str(root));  // Output: 1(2()(4))(3)
    }
}
