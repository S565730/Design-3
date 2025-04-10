# Design-3

## Problem 1: Flatten Nested List Iterator (https://leetcode.com/problems/flatten-nested-list-iterator/)

public class NestedIterator implements Iterator<Integer> {

    Queue<Integer> q = new LinkedList<Integer>();



   public NestedIterator(List<NestedInteger> nestedList) {



       fillQueue(nestedList);



   }



   @Override



   public Integer next() {



       return q.poll();



   }



   @Override



   public boolean hasNext() {



        if(q.isEmpty()) return false;



       return true;



   }



   public void fillQueue(List<NestedInteger> nestList){



       if(nestList == null) return;



       for(NestedInteger li : nestList){



           if(li.isInteger()) q.offer(li.getInteger());



           else



               fillQueue(li.getList());



       }



   }
}




## Problem 2: LRU Cache(https://leetcode.com/problems/lru-cache/)


class LRUCache {

    class Node{


         int key,value;


         Node prev,next;


         public Node(int key,int value){


             this.key=key;


             this.value=value;


         }


         Node(){


             this(0,0);


         }


     }


     Node head,tail;


     Map<Integer,Node> map;


     int capacity,count;


     public LRUCache(int capacity) {


         this.capacity=capacity;


         this.count=0;


         map=new HashMap<>();


         head=new Node();


         tail=new Node();


         head.next=tail;


         tail.prev=head;


     }

     public int get(int key) {


         Node n=map.get(key);


         if(n==null){


             return -1;


         }


         else{


             update(n);


             return n.value;


         }


     }


     public void put(int key, int value) {


         Node n= map.get(key);


         if(n==null){


             n=new Node(key,value);


             map.put(key,n);


             add(n);


             ++count;


         }


         else{


             n.value=value;


             update(n);


         }


         if(count>capacity){


             Node del=tail.prev;


             remove(del);


             map.remove(del.key);


             --count;


         }


     }


     public void update(Node n){


         remove(n);


         add(n);


     }

     public void add(Node node){


         Node after= head.next;


         head.next=node;


         node.prev=head;


         node.next=after;


         after.prev=node;


     }


     public void remove(Node node){


         Node before= node.prev;


         Node after=node.next;


         before.next=after;


         after.prev=before;


     }
}