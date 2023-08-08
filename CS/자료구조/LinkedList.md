# LinkedList 구현


``` java
public class LinkedList<T> {
    private Node<T> head;
    private Node<T> tail;
    private int size = 0;

    private class Node<T> {
        private Node<T> next;
        private T data;

        public Node(T data) {
            this.data = data;
        }
    }

    public Node<T> search(int idx) {
        Node<T> node = head;
        for (int i = 0; i < idx; i++) {
            node = node.next;
        }
        return node;
    }

    public void addFirst(T data) {
        Node<T> newNode = new Node(data);

        newNode.next = head;
        head = newNode;
        size++;

        if(newNode.next == null) {
            tail = head;
        }
    }

    public void add(int idx, T data) {
        if(idx == 0) {
            addFirst(data);
            return;
        }

        Node<T> newNode = new Node<>(data);
        Node<T> tmp = search(idx-1);
        newNode.next = tmp.next;
        tmp.next = newNode;
        size++;

        if(newNode.next == null) {
            tail = newNode;
        }
    }

    public T removeFirst() {
        if(head == null) {
            return null;
        }
        T data = head.data;
        Node<T> tmp = head;
        head = tmp.next;

        tmp = null;
        size--;
        return data;
    }

    public T remove(int idx) {
        if(idx >= size) {
            return null;
        }
        if(idx == 0) {
            return removeFirst();
        }

        Node<T> node = search(idx-1);
        Node<T> deleted = node.next;

        node.next = deleted.next;
        T data = deleted.data;
        deleted = null;
        size--;

        if(node.next == null) {
            tail = node;
        }
        return data;
    }

    public void print() {
        if(head == null) {
            System.out.println("x");
            return;
        }

        Node<T> node = head;
        while(node != null) {
            System.out.print(node.data + " ");
            node = node.next;
        }
        System.out.println();
    }

    public void printInfo() {
        if(size == 0) return;
        System.out.println("head : " + head.data + ",tail : " + tail.data + ",size : " + size);
    }
}
```
