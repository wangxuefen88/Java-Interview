# HashMap与HashTable区别 #

考察点
   1 那个是线程安全的
   2 存储有什么区别
   3 那个效率最好

   A.HashMap是线程不安全的,Hashtable是线程安全的
     `
     //HashTable 使用sync同步锁
     public synchronized V put(K key, V value)
     `
   B.HashMap可以存储key和value的值为null,Hashtable不可以
     `
       //Hashtable如果存储为null,则报错
       if (value == null) {
            throw new NullPointerException();
        }
     `
   C.由于是HashMap没有使用sync,所以效率上高于Hashtable

     