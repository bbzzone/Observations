# Java Data Structures

## Arrays (java.utils.Arrays)

Arrays is a class which contain some methods which can be useful at times. **Most of these methods are applicable on primitive types**

- `Arrays.asList(new int[] {1,2,3,4,5})`

- **Binary Search**

  - `static int binraySearch(int[] array, int key)`
  - `static int binarySearch(int[] array, int fromIndex, int toIndex, int key)`

- **Copying**

  - `static int[] copyOf(int[] array, int newLength)` -> truncate if newLength is less and padding with zeros if new Length is larger than previous length

  - `static T[] copyOf(int [] array, int newLength, class<? extends T[]> newType)`

    - ```java
      Short shortArr[] = new Short[]{5, 2, 15, 52, 10};
      Number[] arr2 = Arrays.copyOf(shortArr, 5, Number[].class);
      ```

  - `static T[] copyOfRange(T[] array, int from, int to)`

    - ```java
      Short arr1[] = new Short[]{15, 10, 45};
      Number[] arr2 = Arrays.copyOfRange(arr1, 1, 3, Number[].class);
      ```

- **To String**

  - `static String deepToString(Object[] object)`
  - `static String toString(Object[] object)`

- **Comparison**

  - `static boolean deepEquals(Object[] object1, Object[] object2)`
  - `static boolean equals(Object[] object1, Object[] object2)`

- **Fill**

  - `static void fill(Object[] array, Object value)` -> will fill value in whole array
  - `static void fill(Object[] array, int fromIndex, int toIndex, Object value)`

- **Hashcode**

  - `static int deepHashCode(Object[] a)`
  - `static int hashCode(Object[] a)`

- **Sort**

  - `static void sort(Object[] object)`
  - `static void sort(Object[] object, int fromIndex, int toIndex)`

## ArrayList

- Constructor

  ```java
  ArrayList<Integer> array = new ArrayList<>();
  // Constructor containing a collection
  ArrayList<String> array2 = new ArrayList<>(Collection C);
  ```

- **Adding Elements**

  - add(element) // append element to the end
  - add (int index, element) // to insert a specific element at a given index
  - addAll (Collection C) // to append all the elements from Collection C
  - addAll (int index, Collection C) // append all the element from Collection to ArrayList from passed index.
  - set(int index, E element) // replace the element at given index with given element
  - clear() // empty the linked list
  - clone() // return a shallow copy of the ArrayList

- **Inquiry**

  - contains(Object obj) // return true if given element in ArrayList Object.

  - size() // returns the size of given array

  - ensureCapacity(int minCapacity) // increase the capacity of ArrayList if required (if minCapacity is greater than current capacity).

  - forEach(action)

    - ```java
      ArrayList<Integer> array = new ArrayList<>();
      array.add(3); array.add(4); array.add(5);
      array.forEach((n) -> System.out.println("value is: " + n));
      ```

  - get(int index) // returns the value at given index

  - indexOf(Object object) // return the index of 1st occurence of the object

  - lastIndexOf(Object object) // return the index of last occurence of the object

  - isEmpty() // returns true if list is empty

- **Remove**

  - remove(int index) // remove the element at given index (this will prioritized if objects are ints)

  - remove (Object object) // remove the 1st occurence of given object

  - removeAll(Collection C) // remove all the elements in the C from arrayList

  - removeIf(Predicate filter) // remove all the elements

    - ```java
      ArrayList<Integer> Numbers = new ArrayList<Integer>();
      Numbers.add(23);
      Numbers.add(32);
      Numbers.add(45);
      Numbers.add(63);
      Numbers.removeIf(n -> (n % 3 == 0));
      ```

  - removeRange(int fromIndex, int toIndex) // remove all the elemets from fromIndex to toIndex

  - retainAll(Collection C) // retain only the elements which are present in this ArrayList

  - subList(int fromIndex, int toIndex) // return a new ArrayList from starting index to ending index

- **Conversion**

  - toArray() // will return an array containg all the elements from ArrayList
  - trimToSize() // will reduce the given capacity of ArrayList to the elements present ni the list
  - toString() // will return the ArrayList as a string

## LinkedList

- Constructor

  ```java
  LinkedList<Integer> ll = new LinkedList<>();
  // Constructor containing a Collection
  LinkedList<String> ll = new LinkedList<>(Collection C);
  // Collection can be anything like ArrayList, sets etc.
  ```

- **Methods (adding element)**

  - add(element) // append element to the end
  - add(int index, E element) // add the element at specific index
  - addAll(int index, Collection<E> c) // add all elements starting from a specific index
  - addAll(Collection<E> c) // append all elements from collection
  - addFirst(element) // add the element at 1st position
  - addLast(element) // add the element at last position
  - clear() // empty the linked list
  - clone() // will return a shallow copy of the list

- **Inquiry**

  - contains(Object obj) // returns true if obj is present in linked list
  - size() // will return the size of the list
  - get(int Index) // will return the element at given index
  - getFirst() // will return the 1st element of the linkedlist
  - getLast() // will return the last element of the linkedList
  - indexOf(Object o) // will return the index of value o, if not present -1
  - lastIndexOf(Object o) // will return the index of last Occurence of o
  - offer(E e) // will add the specific element as tail of the list
  - offerFirst(E e) // will add the specific element at front of the list
  - offerLast(E e) // will add the specific element at last of the list
  - peek() // return the head of the list
  - peekFirst() // will return the 1st element of the list
  - peekLast() // will return the last element of the list

- **Removing Elements**

  - poll() // will remove head of the list
  - pollFirst() // will remove 1st element of the list
  - pollLast() // will remove the last element of the list
  - pop() // will remove an element represented by stack of list
  - push(E e) // will add an element in stack represented by linkedlist
  - remove() // will remove the head of the list
  - remove(int Index) // will remove the element at specific position
  - remove(Object obj) // will remove 1st occurence of element obj
  - removeFirst()
  - removeLast()

- **Conversion**

  - toArray();
  - toString();
