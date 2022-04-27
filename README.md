
# **Merkle Tree**

Merkle tree is a tree data structure with leaf nodes and non leaf nodes. It also known as Hash tree. The reason behind it is it only stores the hashes in its nodes instead of data. In its leaf nodes, it will store the hash of the data. Non leaf nodes contain the hash of its children.

https://user-images.githubusercontent.com/78222170/165585834-4bb6d6b6-59bf-48c8-99e0-ecc2065e9879.png

# **Hash Functions**

A hash or hash-value or a message digest is an array of fixed size random characters  generated when a message  or data is passed through an a  Mathematical algorithm. 

These mathematical algorithms are one way functions meaning, we can generate the output from input but not vice-versa. It has to be deterministic, meaning the input should always maps to same output regardless of the number of times it passed through it.  

*Y(I) = O, where*
**Y**  = Our hash function
**I**  = Input 
**O**  = Output. 

Even a small change in the input produces produces completely output. This property is also known as avalanche effect.

**Y(I') = O'** 

These mathematical algorithms with the above properties are also known as Hash Functions.
