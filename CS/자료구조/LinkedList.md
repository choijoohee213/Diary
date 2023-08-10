# LinkedList 구현


``` java
public class LinkedList<E> {
    private Node<E> head;
    private Node<E> tail;
    private int size = 0;

    private class Node<E> {
        private Node<E> next;
        private E data;

        public Node(E data) {
            this.data = data;
        }
    }

    public Node<E> search(int idx) {  //idx번째 있는 노드 반환
        if(idx >= size) {
            throw new IndexOutOfBoundsException();
        }
        Node<E> node = head;
        for (int i = 0; i < idx; i++) {
            node = node.next;
        }
        return node;
    }

    public void addFirst(E data) {  //맨 앞에 노드 추가
        Node<E> newNode = new Node(data);

        newNode.next = head;
        head = newNode;
        size++;

        if(newNode.next == null) {
            tail = head;
        }
    }

    public void add(int idx, E data) {  //idx번째에 노드 추가
        if(idx == 0) {
            addFirst(data);
            return;
        }

        Node<E> newNode = new Node<>(data);
        Node<E> tmp = search(idx-1);
        newNode.next = tmp.next;
        tmp.next = newNode;
        size++;

        if(newNode.next == null) {
            tail = newNode;
        }
    }

    public E removeFirst() {  //맨 앞 노드 삭제
        if(head == null) {
            throw new IndexOutOfBoundsException();
        }
        E data = head.data;
        Node<E> tmp = head;
        head = tmp.next;

        tmp = null;
        size--;
        return data;
    }

    public E remove(int idx) {  //idx번째에 있는 노드 삭제
        if(idx >= size) {
            throw new IndexOutOfBoundsException();
        }
        if(idx == 0) {
            return removeFirst();
        }

        Node<E> node = search(idx-1);
        Node<E> deleted = node.next;

        node.next = deleted.next;
        E data = deleted.data;
        deleted = null;
        size--;

        if(node.next == null) {
            tail = node;
        }
        return data;
    }

    public void print() {  //모든 노드의 데이터 순서대로 출력
        if(head == null) {
            System.out.println("x");
            return;
        }

        Node<E> node = head;
        while(node != null) {
            System.out.print(node.data + " ");
            node = node.next;
        }
        System.out.println();
    }

    public void printInfo() {  //현재 head, tail의 데이터와 size 출력
        if(size == 0) return;
        System.out.println("head : " + head.data + ",tail : " + tail.data + ",size : " + size);
    }
}
```
