## 자바로 Queue 구현하기

```java
public class MyQueue{
    private static class QueueNode {
        private T data;
        private QueueNode next;

        public QueueNode(T data){
            this.data = data;
        };
    }

    private QueueNode first;
    private QueueNode last;

    public void add(T item){
        QueueNode t = new QueueNode(item);
        if(last != null) last.next = t;
        last = t;
        if(first == null) first = last;
    }

    public T remove(){
        if(first == null) throw new NoSuchElementException();

        T item = first.data;
        first = first.next; 

        if (first == null) last = null;
        return item;
    }

    public T peek(){
        if (first == null) throw new NosuchElementException();
        return fisrt.data;
    }
    
    public boolean isEmpty(){
        return first == null;
    }

```