
# **Merkle Tree**

Merkle tree is a tree data structure with leaf nodes and non leaf nodes. It also known as Hash tree. The reason behind it is it only stores the hashes in its nodes instead of data. In its leaf nodes, it will store the hash of the data. Non leaf nodes contain the hash of its children.

```
Merkle Tree is a USPTO patented Algorithm/ Data Structure and hence, you cannot use it in production without permission or by paying royality to Ralph Merkle. Merkle Tree is also known as Hash Tree.
```

# **Architecture of Merkle Tree**
![](https://user-images.githubusercontent.com/78222170/165585834-4bb6d6b6-59bf-48c8-99e0-ecc2065e9879.png)

# **Hash Functions**

A hash or hash-value or a message digest is an array of fixed size random characters  generated when a message  or data is passed through an a  Mathematical algorithm. 

These mathematical algorithms are one way functions meaning, we can generate the output from input but not vice-versa. It has to be deterministic, meaning the input should always maps to same output regardless of the number of times it passed through it.  

***Y(I) = O, where*** <br />
**Y**  = Our hash function <br />
**I**  = Input <br />
**O**  = Output. <br />

Even a small change in the input produces produces completely output. This property is also known as avalanche effect.

**Y(I') = O'** 

These mathematical algorithms with the above properties are also known as Hash Functions.

# **Merkle Tree Implementation in Java**
In this example implementation, We are going to implement binary merkle tree. As the first step, let's define the node. Like a regular tree, it has a data field to store the hash and left and right pointers to point to left child and right child of the binary tree.
```java
public class Node {

    private Node left;
    private Node right;
    private String hash;

    public Node(Node left, Node right, String hash) {
        this.left = left;
        this.right = right;
        this.hash = hash;
    }

    public Node getLeft() {
        return left;
    }

    public void setLeft(Node left) {
        this.left = left;
    }

    public Node getRight() {
        return right;
    }

    public void setRight(Node right) {
        this.right = right;
    }

    public String getHash() {
        return hash;
    }

    public void setHash(String hash) {
        this.hash = hash;
    }
}
```

# **Code**
We are going to implement a complete binary tree. In case of odd nodes, we will consider the odd node twice to generate the hash of its parent.

```java
package com.merkle.tree.implementation;

import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

public class MerkleTree {
    public static Node treegen(ArrayList<String> infor) {
        ArrayList<Node> childnodes = new ArrayList<>();
        for (String message : infor) {
            childnodes.add(new Node(null, null, hashalg.generateHash(message)));
        }
        return buildTree(childnodes);
    }
    private static Node buildTree(ArrayList<Node> children) {
        ArrayList<Node> parents = new ArrayList<>();
        while (children.size() != 1) {
            int index = 0, length = children.size();
            while (index < length) {
                Node leftChild = children.get(index);
                Node rightChild = null;
                if ((index + 1) < length) {
                    rightChild = children.get(index + 1);
                } else {
                    rightChild = new Node(null, null, leftChild.getHash());
                }
                String parentHash = hashalg.generateHash(leftChild.getHash() + rightChild.getHash());
                parents.add(new Node(leftChild, rightChild, parentHash));
                index += 2;
            }
            children = parents;
            parents = new ArrayList<>();
        }
        return children.get(0);
    }
    private static void printLevelOrderTraversal(Node root) {
        if (root == null) {
            return;
        }
        if ((root.getLeft() == null && root.getRight() == null)) {
            System.out.println(root.getHash());
        }
        Queue<Node> queue = new LinkedList<>();
        queue.add(root);
        queue.add(null);

        while (!queue.isEmpty()) {
            Node node = queue.poll();
            if (node != null) {
                System.out.println(node.getHash());
            } else {
                System.out.println();
                if (!queue.isEmpty()) {
                    queue.add(null);
                }
            }
            if (node != null && node.getLeft() != null) {
                queue.add(node.getLeft());
            }
            if (node != null && node.getRight() != null) {
                queue.add(node.getRight());
            }
        }
    }
    public static void main(String[] args) {
        ArrayList<String> infor = new ArrayList<>();
        infor.add("Thermite");
        infor.add("Fuze");
        infor.add("Tachanka");
        infor.add("Ace");
		infor.add("Vigil");
        Node root = treegen(infor);
        printLevelOrderTraversal(root);
    }
}
```
# **References**

```
https://www.pranaybathini.com/2021/05/merkle-tree.html
```
