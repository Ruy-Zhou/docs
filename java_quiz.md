### Question 1: Implement a Binary Search Tree
Write a class to implement a binary search tree (BST) with methods for insertion, search, and in-order traversal.

```java
class BinarySearchTree {
   TreeNode root = null;

   BinarySearchTree() {
   }

   void insert(int var1) {
      this.root = this.insertRec(this.root, var1);
   }

   TreeNode insertRec(TreeNode var1, int var2) {
      if (var1 == null) {
         var1 = new TreeNode(var2);
         return var1;
      } else {
         if (var2 < var1.value) {
            var1.left = this.insertRec(var1.left, var2);
         } else if (var2 > var1.value) {
            var1.right = this.insertRec(var1.right, var2);
         }

         return var1;
      }
   }

   boolean search(int var1) {
      return this.searchRec(this.root, var1);
   }

   boolean searchRec(TreeNode var1, int var2) {
      if (var1 == null) {
         return false;
      } else if (var1.value == var2) {
         return true;
      } else {
         return var2 < var1.value ? this.searchRec(var1.left, var2) : this.searchRec(var1.right, var2);
      }
   }

   void inorder() {
      this.inorderRec(this.root);
   }

   void inorderRec(TreeNode var1) {
      if (var1 != null) {
         this.inorderRec(var1.left);
         System.out.print(var1.value + " ");
         this.inorderRec(var1.right);
      }

   }

   public static void main(String[] var0) {
      BinarySearchTree var1 = new BinarySearchTree();
      var1.insert(50);
      var1.insert(30);
      var1.insert(20);
      var1.insert(40);
      var1.insert(70);
      var1.insert(60);
      var1.insert(80);
      var1.inorder();
      System.out.println(var1.search(40));
      System.out.println(var1.search(90));
   }
}
```

### Question 2: Implement a Stack Using Arrays
Write a class to implement a stack using arrays with methods for push, pop, and peek.

```java
public class Stack {
    private int[] elements;
    private int top;
    private static final int DEFAULT_SIZE = 10; // Default size of the stack array;

    public Stack() {
        this(DEFAULT_SIZE); // Call the constructor with the default size
    }
    public Stack(int initialSize) {
        if (initialSize <= 0) {
            throw new IllegalArgumentException("Initial size must be greater than zero"); 
        }

        this.elements = new int[initialSize];
        top = -1; // Initialize top to -1 to indicate an empty stack
    }
    // dynmically resize the stack array when it is full
    public void resize(int newSize) {
        if (newSize <= 0) {
            throw new IllegalArgumentException("New size must be greater than zero");
        }

        int[] newElements = new int[newSize];
        System.arraycopy(elements, 0, newElements, 0, Math.min(elements.length, newSize));
        elements = newElements;
    }

    public void push(int element) {
        if (top == elements.length - 1) {
            resize(elements.length * 2); // Double the size of the stack array if it is full
        } else {
            elements[++top] = element; // Increment top and add element to the stack
        }
    }

    public int pop() {
        if (top == -1) {
            System.out.println("Stack is empty");
            return -1; // Return -1 to indicate an empty stack 
        }

        return elements[top--]; // Return the element at top and decrement top
    }

    public int peek() {
        if (top == -1) {
            System.out.println("Stack is empty");
            return -1; // Return -1 to indicate an empty stack
        }

        return elements[top]; // Return the element at top without removing it
    }

    public boolean isEmpty() {
        return top == -1; // Check if the stack is empty
    }

    public int size() {
        return top + 1; // Return the number of elements in the stack 
    }

    public static void main(String[] args) {
        Stack stack = new Stack(5);
        stack.push(10);
        stack.push(20);
        stack.push(30);

        System.out.println(stack.peek());  // Output: 30
        System.out.println(stack.pop());   // Output: 30
        System.out.println(stack.pop());   // Output: 20
        System.out.println(stack.pop());   // Output: 10
        System.out.println(stack.pop());   // Output: Stack is empty
    }
}
```

### Question 3: Implement a Queue Using Linked Lists
Write a class to implement a queue using linked lists with methods for enqueue, dequeue, and peek.

```java
class Node {
    int value;
    Node next;

    public Node(int value) {
        this.value = value;
        this.next = null; 
    }
}


public class Queue {
    private Node head, tail; // front and rear pointers to the first and last nodes in the queue, respectively.
    private Node[] elements; // size of the queue.
    private static final int DEFAULT_SIZE = 10; // Default size of the stack array;
    private int size;

    public Queue() {
        this(DEFAULT_SIZE); // Call the constructor with the default size
    }

    public Queue(int initialSize) {
        if (initialSize <= 0) {
            throw new IllegalArgumentException("Initial size must be greater than zero"); 
        }

        this.elements = new Node[initialSize];
        head = tail = null; // Initialize head and tail to -1 to indicate an empty queue
    }

    public void enqueue(int value) {
        if (isFull()) {
            System.out.println("Queue is full");
        }

        Node newNode = new Node(value); // Create a new node with the given value.

        if (isEmpty()) { // If the queue is empty, set both head and tail to the new node.
            head = tail = newNode;
        } else { 
            tail.next = newNode; 
            tail = newNode; 
        }

        size++;
    }

    public int dequeue() {
        if (isEmpty()) {
            System.out.println("Queue is empty");
            return -1; // Return -1 to indicate an empty stack
        }

        int value = head.value;
        head = head.next; // Move the head pointer to the next node.

        size--;

        if (head == null) { // If the queue becomes empty, set tail to null.
            tail = null;
        }

        return value;
    }

    public int peek() {
        if (isEmpty()) {
            System.out.println("Queue is empty");
        }

        return head.value;
    }

    public boolean isFull() {
        return size == elements.length; // Check if the queue is full
    }

    public boolean isEmpty() {
        return size == 0; // Check if the queue is empty 
    }
    
    public static void main(String[] args) {
        Queue queue = new Queue();
        queue.enqueue(10);
        queue.enqueue(20);
        queue.enqueue(30);

        System.out.println(queue.peek());  // Output: 10
        System.out.println(queue.dequeue());  // Output: 10
        System.out.println(queue.dequeue());  // Output: 20
        System.out.println(queue.dequeue());  // Output: 30
        System.out.println(queue.dequeue());  // Output: Queue is empty
    }
}
```
