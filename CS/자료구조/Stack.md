# Stack 구현
Stack을 배열과 링크드리스트 두가지로 구현해보기


### Stack 인터페이스
``` java
public interface Stack<E> {
    boolean add(E data);
    E pop();
    E peek();
    E get(int idx);
    boolean isEmpty();
    void clear();
}
```

### ArrayStack (배열 이용)
``` java
import java.util.Arrays;

public class ArrayStack<E> implements Stack<E> {
    private final int initCapacity = 100;
    private Object[] arr = new Object[initCapacity];
    private int size = 0;

    private void increaseCapacity() {
        int newSize = arr.length + initCapacity;
        arr = Arrays.copyOf(arr, newSize);
    }

    @Override
    public boolean add(E data) {
        if(size >= arr.length-1) {
            increaseCapacity();
        }

        arr[size++] = data;
        return true;
    }

    @Override
    public E pop() {
        E data = (E) arr[--size];
        arr[size] = 0;
        return data;
    }

    @Override
    public E peek() {
        return (E) arr[size-1];
    }

    @Override
    public E get(int idx) {
        if(idx >= size) {
            throw new ArrayIndexOutOfBoundsException();
        }
        return (E) arr[idx];
    }

    @Override
    public boolean isEmpty() {
        return size == 0;
    }

    @Override
    public void clear() {
        size = 0;
        arr = new Object[initCapacity];
    }
}

```

### LinkedListStack (링크드리스트 이용)
``` java
public class LinkedListStack<E> implements Stack<E> {
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

    public Node<E> search(int idx) {
        if(size <= idx) return null;
        Node node = head;

        for (int i = 0; i < idx; i++) {
            node = node.next;
        }

        return node;
    }

    @Override
    public boolean add(E data) {
        Node<E> newNode = new Node<>(data);

        if(tail == null) {
            head = newNode;
            tail = newNode;
        } else {
            tail.next = newNode;
            tail = newNode;
        }
        size++;
        return true;
    }

    @Override
    public E pop() {
        Node<E> deleted = tail;
        E data = deleted.data;

        if(size == 1) {
            head = null;
            tail = null;
        } else {
            Node<E> node = search(size - 2);
            node.next = null;
            tail = node;
        }
        deleted = null;
        size--;
        return data;
    }

    @Override
    public E peek() {
        return tail.data;
    }

    @Override
    public E get(int idx) {
        return search(idx).data;
    }

    @Override
    public boolean isEmpty() {
        return size == 0;
    }

    @Override
    public void clear() {
        Node<E> node = head;

        while(node != null) {
            Node<E> tmp = node;
            node = node.next;
            tmp = null;
        }
        head = null;
        tail = null;
        size = 0;
    }
}

```
