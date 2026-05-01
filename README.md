# Swift ile Veri Yapıları ve Algoritmaları Roadmap

Bu roadmap, Swift kullanarak veri yapıları ve algoritmalar konusunda sıfırdan ileri seviyeye kontrollü şekilde ilerlemek için hazırlanmıştır. Amaç sadece problem çözmek değil; her yapıyı Swift ile implement etmek, karmaşıklık analizini öğrenmek, farklı problem kalıplarını tanımak, düzenli tekrar yapmak ve ilerlemeyi günlük olarak ölçmektir.

Program varsayılan olarak **24 hafta** tasarlanmıştır. Daha yoğun çalışılırsa 12-16 haftaya sıkıştırılabilir; daha sürdürülebilir çalışılırsa 6-9 aya yayılabilir.

---

## 1. Genel Hedefler

Program sonunda şu seviyeye gelmiş olmalısın:

* Big-O analizini pratik olarak yapabilmek.
* Array, Linked List, Stack, Queue, Hash Table, Tree, Heap, Graph, Trie, Union-Find gibi temel yapıları Swift ile yazabilmek.
* Sorting, Searching, Recursion, Backtracking, Greedy, Divide and Conquer, Dynamic Programming, Graph Traversal gibi algoritma ailelerini tanıyıp uygulayabilmek.
* LeetCode / HackerRank / CodeSignal tarzı platformlarda orta seviye problemleri sistematik çözebilmek.
* iOS geliştirmede kullanılan gerçek veri yapısı kararlarını daha bilinçli verebilmek.
* Interview seviyesinde problem çözümünü açıklayabilmek: brute force → optimize çözüm → karmaşıklık analizi → edge case.

---

## 2. Günlük Çalışma Sistemi

Her gün minimum bir çalışma döngüsü yapılmalı.

### Günlük minimum plan: 60-90 dakika

1. **10 dk tekrar**

   * Önceki günün konusu.
   * Zaman karmaşıklığı notları.
   * Çözülen problemlerden çıkarılan kalıplar.

2. **20-30 dk konu öğrenme**

   * Teorik yapı / algoritma.
   * Swift karşılığı.
   * Standart library davranışı.

3. **20-30 dk implementasyon**

   * Veri yapısını veya algoritmayı Swift ile sıfırdan yaz.
   * Generic kullan.
   * Unit test ekle.

4. **20-40 dk problem çözme**

   * En az 1 problem.
   * Zor günlerde sadece çözüm analizi yapılabilir.

5. **5 dk günlük log**

   * Bugün ne öğrendim?
   * Hangi problemde takıldım?
   * Hangi kalıp tekrar karşıma çıktı?
   * Yarın neye devam edeceğim?

### Yoğun plan: 2-3 saat

* 20 dk tekrar
* 40 dk konu
* 40 dk implementasyon
* 60 dk problem çözme
* 10 dk not / log

---

## 3. Günlük Takip Şablonu

Her gün aşağıdaki formatla ilerleme kaydı tutulmalı.

```markdown
## Gün: YYYY-MM-DD

### Çalışılan konu
-

### Implementasyon
-

### Çözülen problemler
1.
2.
3.

### Bugünkü Big-O notları
-

### Takıldığım noktalar
-

### Öğrendiğim kalıplar
-

### Yarınki hedef
-

### Günlük puan
- Konu: /2
- Kodlama: /2
- Problem: /3
- Analiz: /2
- Tekrar: /1
- Toplam: /10
```

### Günlük başarı kriteri

* 6/10: Minimum kabul edilebilir gün.
* 8/10: İyi gün.
* 10/10: Tam çalışma günü.

Haftada 5 gün 6+ puan hedeflenmeli.

---

## 4. Haftalık Takip Şablonu

Her hafta sonunda kısa değerlendirme yapılmalı.

```markdown
## Hafta Özeti

### Bu hafta çalışılan konular
-

### Implement edilen yapılar / algoritmalar
-

### Çözülen problem sayısı
- Easy:
- Medium:
- Hard:

### En çok zorlanılan kalıp
-

### Tekrar edilmesi gereken konular
-

### Haftalık mini proje
-

### Sonraki hafta hedefleri
-
```

---

## 5. Swift Odaklı Temel Prensipler

### 5.1 Value Semantics

Swift koleksiyonları genellikle value type davranışı gösterir. Array, Dictionary, Set gibi yapılar copy-on-write optimizasyonu kullanır. Veri yapısı implement ederken şu konular bilinmeli:

* `struct` vs `class`
* Copy-on-write
* Mutating methods
* Reference cycles
* Generic constraints
* Protocol oriented design

### 5.2 Generics

Veri yapıları çoğunlukla generic yazılmalı.

```swift
struct Stack<Element> {
    private var storage: [Element] = []

    mutating func push(_ element: Element) {
        storage.append(element)
    }

    mutating func pop() -> Element? {
        storage.popLast()
    }

    var peek: Element? {
        storage.last
    }

    var isEmpty: Bool {
        storage.isEmpty
    }
}
```

### 5.3 Comparable ve Hashable

Sorting, Heap, Binary Search Tree, Set, Dictionary ve Hash Table problemleri için önemli.

```swift
func binarySearch<T: Comparable>(_ array: [T], target: T) -> Int? {
    var left = 0
    var right = array.count - 1

    while left <= right {
        let mid = left + (right - left) / 2
        if array[mid] == target { return mid }
        if array[mid] < target {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }

    return nil
}
```

### 5.4 Swift Standard Library Bilinmesi Gerekenler

* `Array`
* `Dictionary`
* `Set`
* `Deque` yok; queue için custom yapı yazmak gerekir.
* `sort()` ve `sorted()` farkı.
* `map`, `filter`, `reduce`, `compactMap`, `flatMap`.
* `String` indeksleme maliyetleri.
* `Character`, `UnicodeScalar`, `String.Index`.

---

## 6. Problem Çözme Metodu

Her problem için aynı akış kullanılmalı.

### 6.1 Analiz akışı

1. Problemi kendi cümlelerinle yeniden yaz.
2. Input / output örneklerini elle çöz.
3. Constraintleri oku.
4. Brute force çözümü tasarla.
5. Zaman ve alan karmaşıklığını yaz.
6. Optimize etmek için veri yapısı seç.
7. Edge caseleri listele.
8. Swift kodunu yaz.
9. Test et.
10. Alternatif çözümü not al.

### 6.2 Problem not formatı

```markdown
# Problem Adı

## Pattern
Two Pointers / Hash Map / DP / Graph / vb.

## Brute Force
Açıklama

## Optimize Çözüm
Açıklama

## Complexity
Time: O(...)
Space: O(...)

## Edge Cases
-

## Swift Notu
-

## Tekrar Tarihi
-
```

---

# 24 Haftalık Roadmap

---

## Faz 1: Temel Analiz ve Swift Hazırlığı

### Hafta 1: Big-O, Swift Temelleri ve Problem Çözme Disiplini

#### Konular

* Time complexity
* Space complexity
* Big-O, Big-Theta, Big-Omega
* Best / average / worst case
* Constant, logarithmic, linear, linearithmic, quadratic, exponential karmaşıklıklar
* Swift Array, Dictionary, Set karmaşıklıkları
* Mutability
* Value vs reference types

#### Implementasyon

* Basit benchmark helper
* Array traversal örnekleri
* Nested loop analizleri
* Binary search helper

#### Problemler

* Running Sum of 1d Array
* Richest Customer Wealth
* Fizz Buzz
* Number of Steps to Reduce a Number to Zero
* Binary Search
* First Bad Version

#### Hedef

Big-O notasyonu sezgisel değil, mekanik olarak çıkarılabilir hale gelmeli.

---

### Hafta 2: Array ve String Temelleri

#### Konular

* Array traversal
* Prefix sum
* Sliding window giriş
* In-place update
* String indexing in Swift
* Character frequency
* Mutable arrays

#### Implementasyon

* Dynamic array mantığını simüle et
* Prefix sum struct
* Frequency counter
* String character scanner

#### Problemler

* Two Sum
* Contains Duplicate
* Best Time to Buy and Sell Stock
* Valid Anagram
* Move Zeroes
* Merge Sorted Array
* Squares of a Sorted Array
* Find Pivot Index

#### Swift notları

* `String` doğrudan integer index ile erişilemez.
* String problemlerinde gerekirse `Array(s)` dönüşümü yapılır; bunun O(n) maliyeti vardır.

---

### Hafta 3: Two Pointers ve Sliding Window

#### Konular

* Opposite direction two pointers
* Same direction two pointers
* Fixed-size sliding window
* Variable-size sliding window
* Window shrink / expand mantığı

#### Implementasyon

* Generic two pointer helpers
* Fixed window max sum
* Variable window longest substring

#### Problemler

* Valid Palindrome
* Two Sum II
* 3Sum
* Container With Most Water
* Remove Duplicates from Sorted Array
* Maximum Average Subarray I
* Longest Substring Without Repeating Characters
* Minimum Size Subarray Sum
* Permutation in String

#### Hedef

Array ve string problemlerinde O(n²) çözümleri O(n) seviyesine çekebilmek.

---

## Faz 2: Lineer Veri Yapıları

### Hafta 4: Stack

#### Konular

* LIFO
* Call stack
* Monotonic stack
* Parentheses matching
* Expression evaluation

#### Implementasyon

* Generic Stack
* MinStack
* Monotonic increasing stack
* Monotonic decreasing stack

#### Problemler

* Valid Parentheses
* Min Stack
* Baseball Game
* Daily Temperatures
* Next Greater Element I
* Evaluate Reverse Polish Notation
* Remove All Adjacent Duplicates In String

#### Mini proje

* Swift ile expression validator yaz.
* Girdi: string expression.
* Çıktı: geçerli/geçersiz, hata pozisyonu.

---

### Hafta 5: Queue, Deque ve BFS Hazırlığı

#### Konular

* FIFO
* Queue implementasyon teknikleri
* Array `removeFirst()` maliyeti
* Head index optimizasyonu
* Circular buffer
* Deque mantığı

#### Implementasyon

* Queue with array and head index
* CircularQueue
* Deque
* Moving average from data stream

#### Problemler

* Implement Queue using Stacks
* Implement Stack using Queues
* Number of Recent Calls
* Moving Average from Data Stream
* Design Circular Queue
* Walls and Gates

#### Swift notu

`Array.removeFirst()` O(n) olabilir. Queue implementasyonunda head pointer kullan.

---

### Hafta 6: Linked List

#### Konular

* Singly linked list
* Doubly linked list
* Dummy node
* Fast and slow pointers
* Cycle detection
* Reverse list
* Merge lists

#### Implementasyon

* Node class
* SinglyLinkedList
* DoublyLinkedList
* Reverse linked list
* Detect cycle

#### Problemler

* Reverse Linked List
* Middle of the Linked List
* Linked List Cycle
* Merge Two Sorted Lists
* Remove Nth Node From End of List
* Palindrome Linked List
* Add Two Numbers
* Intersection of Two Linked Lists

#### Swift notları

* Node çoğunlukla `class` olur; referans semantiği gerekir.
* Retain cycle riskine dikkat et; doubly linked list'te `weak var previous` kullanılabilir.

---

## Faz 3: Hashing ve Set Tabanlı Çözümler

### Hafta 7: Hash Table, Dictionary, Set

#### Konular

* Hash function
* Collision
* Load factor
* Separate chaining
* Open addressing
* Dictionary complexity
* Set membership

#### Implementasyon

* Simple HashMap
* HashSet
* Frequency map helper
* Grouping helper

#### Problemler

* Two Sum
* Group Anagrams
* Top K Frequent Elements
* Longest Consecutive Sequence
* Isomorphic Strings
* Word Pattern
* Subarray Sum Equals K
* First Unique Character in a String

#### Mini proje

* Basit LRU cache öncesi key-value store yaz.

---

### Hafta 8: Advanced Hashing Patterns

#### Konular

* Prefix sum + HashMap
* Frequency comparison
* Counting patterns
* Hashing with tuples
* Custom Hashable types

#### Implementasyon

* PrefixFrequencyMap
* Custom coordinate hash
* Pair hash modelleme

#### Problemler

* Subarray Sum Equals K
* Contiguous Array
* Longest Harmonious Subsequence
* Find All Anagrams in a String
* Minimum Window Substring
* Valid Sudoku
* Encode and Decode Strings

#### Hedef

“Bir şeyi daha önce gördüm mü?”, “kaç kere gördüm?”, “hangi indexte gördüm?” sorularında otomatik olarak Dictionary / Set düşünebilmek.

---

## Faz 4: Sorting ve Searching

### Hafta 9: Sorting Algoritmaları

#### Konular

* Bubble sort
* Selection sort
* Insertion sort
* Merge sort
* Quick sort
* Heap sort
* Stable vs unstable sort
* In-place sorting

#### Implementasyon

* Bubble sort
* Insertion sort
* Merge sort
* Quick sort
* Generic sort helpers

#### Problemler

* Sort Colors
* Merge Intervals
* Insert Interval
* Non-overlapping Intervals
* Meeting Rooms
* Meeting Rooms II
* Largest Number

#### Swift notu

* `sort()` array'i yerinde değiştirir.
* `sorted()` yeni array döndürür.

---

### Hafta 10: Binary Search ve Search Space Reduction

#### Konular

* Classic binary search
* Lower bound
* Upper bound
* Search insert position
* Binary search on answer
* Rotated sorted array

#### Implementasyon

* `lowerBound`
* `upperBound`
* Generic binary search
* Predicate based binary search

#### Problemler

* Binary Search
* Search Insert Position
* First Bad Version
* Search in Rotated Sorted Array
* Find Minimum in Rotated Sorted Array
* Find First and Last Position of Element
* Koko Eating Bananas
* Capacity To Ship Packages Within D Days

#### Hedef

Sadece sorted array'de değil, cevap aralığında da binary search kullanabilmek.

---

## Faz 5: Recursion, Backtracking, Divide and Conquer

### Hafta 11: Recursion

#### Konular

* Base case
* Recursive case
* Call stack
* Tail recursion
* Recursion tree
* Memoization giriş

#### Implementasyon

* Factorial
* Fibonacci naive / memoized
* Recursive binary search
* Tree-like recursion examples

#### Problemler

* Fibonacci Number
* Climbing Stairs
* Pow(x, n)
* Merge Sort
* Reverse String
* Pascal's Triangle

#### Hedef

Recursion tree çizerek zaman karmaşıklığı çıkarabilmek.

---

### Hafta 12: Backtracking

#### Konular

* Choice / explore / unchoose
* State space tree
* Pruning
* Combinations
* Permutations
* Subsets
* Constraint solving

#### Implementasyon

* Subsets generator
* Permutations generator
* Combination generator
* N-Queens solver

#### Problemler

* Subsets
* Subsets II
* Permutations
* Permutations II
* Combinations
* Combination Sum
* Letter Combinations of a Phone Number
* Generate Parentheses
* Word Search
* N-Queens

#### Hedef

Backtracking template'i ezberlemek değil, state yönetimini doğru kurmak.

---

### Hafta 13: Divide and Conquer

#### Konular

* Problem parçalama
* Combine step
* Master theorem giriş
* Recursive sortlar
* Quickselect

#### Implementasyon

* Merge sort
* Quick sort
* Quickselect
* Count inversions

#### Problemler

* Kth Largest Element in an Array
* Majority Element
* Maximum Subarray
* Search a 2D Matrix II
* Count of Smaller Numbers After Self

---

## Faz 6: Ağaçlar

### Hafta 14: Binary Tree Temelleri

#### Konular

* Tree terminology
* Root, child, parent, leaf
* Height, depth
* DFS preorder / inorder / postorder
* BFS level order
* Recursive traversal
* Iterative traversal

#### Implementasyon

* BinaryTreeNode
* DFS recursive
* DFS iterative
* BFS level order
* Tree height
* Tree size

#### Problemler

* Maximum Depth of Binary Tree
* Same Tree
* Invert Binary Tree
* Binary Tree Level Order Traversal
* Diameter of Binary Tree
* Balanced Binary Tree
* Symmetric Tree
* Path Sum

#### Swift notu

Tree node genellikle `class` olur.

---

### Hafta 15: Binary Search Tree

#### Konular

* BST invariant
* Insert
* Search
* Delete
* Min / max
* Inorder sorted output
* Validate BST

#### Implementasyon

* BinarySearchTree
* Insert/search/delete
* Inorder iterator

#### Problemler

* Validate Binary Search Tree
* Lowest Common Ancestor of a BST
* Kth Smallest Element in a BST
* Convert Sorted Array to Binary Search Tree
* Insert into a BST
* Delete Node in a BST

#### Hedef

BST invariant'ını her recursive çağrıda koruyabilmek.

---

### Hafta 16: Advanced Tree Patterns

#### Konular

* Lowest common ancestor
* Path problems
* Serialization
* Tree DP giriş
* Trie hazırlığı

#### Implementasyon

* Serialize / deserialize binary tree
* LCA generic tree
* Path collector

#### Problemler

* Binary Tree Maximum Path Sum
* Serialize and Deserialize Binary Tree
* Construct Binary Tree from Preorder and Inorder Traversal
* Lowest Common Ancestor of Binary Tree
* Flatten Binary Tree to Linked List
* Sum Root to Leaf Numbers

---

## Faz 7: Heap, Priority Queue, Trie

### Hafta 17: Heap ve Priority Queue

#### Konular

* Min heap
* Max heap
* Heap insert
* Heap remove
* Heapify
* Priority queue
* Top-K pattern
* Streaming median

#### Implementasyon

* Generic Heap
* PriorityQueue
* MinHeap / MaxHeap wrappers

#### Problemler

* Kth Largest Element in an Array
* Top K Frequent Elements
* Find Median from Data Stream
* Merge K Sorted Lists
* Task Scheduler
* Last Stone Weight
* K Closest Points to Origin

#### Swift notu

Swift standard library'de built-in PriorityQueue yoktur; custom implementasyon gerekir.

---

### Hafta 18: Trie

#### Konular

* Prefix tree
* Word search
* Auto-complete
* Dictionary tree
* Memory trade-off

#### Implementasyon

* TrieNode
* Trie insert/search/startsWith
* Auto-complete

#### Problemler

* Implement Trie
* Word Search II
* Design Add and Search Words Data Structure
* Replace Words
* Longest Word in Dictionary
* Search Suggestions System

#### Mini proje

* Basit autocomplete engine.

---

## Faz 8: Graph Algorithms

### Hafta 19: Graph Temelleri, BFS, DFS

#### Konular

* Directed / undirected graph
* Weighted / unweighted graph
* Adjacency list
* Adjacency matrix
* BFS
* DFS
* Connected components
* Cycle detection

#### Implementasyon

* Graph adjacency list
* BFS
* DFS recursive / iterative
* Connected component counter

#### Problemler

* Number of Islands
* Clone Graph
* Max Area of Island
* Flood Fill
* Rotting Oranges
* Pacific Atlantic Water Flow
* Surrounded Regions

#### Hedef

Grid problemlerini graph problemi olarak modelleyebilmek.

---

### Hafta 20: Topological Sort ve Union-Find

#### Konular

* DAG
* In-degree
* Kahn algorithm
* DFS based topological sort
* Union-Find
* Path compression
* Union by rank / size

#### Implementasyon

* Topological sort
* DisjointSetUnion
* Cycle detection with DSU

#### Problemler

* Course Schedule
* Course Schedule II
* Alien Dictionary
* Redundant Connection
* Graph Valid Tree
* Number of Connected Components in an Undirected Graph
* Accounts Merge

---

### Hafta 21: Shortest Path ve Weighted Graphs

#### Konular

* Dijkstra
* Bellman-Ford giriş
* Floyd-Warshall giriş
* Minimum spanning tree giriş
* Priority queue ile graph

#### Implementasyon

* Dijkstra with PriorityQueue
* WeightedGraph
* ShortestPathResult

#### Problemler

* Network Delay Time
* Cheapest Flights Within K Stops
* Path With Minimum Effort
* Swim in Rising Water
* Min Cost to Connect All Points

#### Hedef

Unweighted graph'ta BFS, weighted positive graph'ta Dijkstra refleksi kazanmak.

---

## Faz 9: Greedy ve Dynamic Programming

### Hafta 22: Greedy Algorithms

#### Konular

* Local optimum
* Global optimum
* Sorting + greedy
* Interval greedy
* Proof intuition

#### Implementasyon

* Interval scheduling
* Activity selection
* Greedy coin change örneği

#### Problemler

* Assign Cookies
* Jump Game
* Jump Game II
* Gas Station
* Partition Labels
* Non-overlapping Intervals
* Minimum Number of Arrows to Burst Balloons
* Queue Reconstruction by Height

#### Hedef

Greedy çözümün neden doğru olduğunu açıklayabilmek.

---

### Hafta 23: Dynamic Programming Temelleri

#### Konular

* Overlapping subproblems
* Optimal substructure
* Top-down memoization
* Bottom-up tabulation
* State definition
* Transition
* Base case

#### Implementasyon

* Fibonacci memoized / tabulated
* Climbing stairs
* House robber
* Coin change

#### Problemler

* Climbing Stairs
* House Robber
* House Robber II
* Min Cost Climbing Stairs
* Coin Change
* Maximum Subarray
* Decode Ways
* Word Break

#### DP çözüm formatı

```markdown
State:
dp[i] = ...

Transition:
dp[i] = ...

Base Case:
...

Order:
...

Answer:
...
```

---

### Hafta 24: Advanced DP ve Final Review

#### Konular

* 2D DP
* Knapsack
* Longest common subsequence
* Palindromic DP
* Interval DP giriş
* DP optimization giriş

#### Implementasyon

* 0/1 Knapsack
* LCS
* Edit Distance
* Longest Palindromic Subsequence

#### Problemler

* Longest Increasing Subsequence
* Longest Common Subsequence
* Edit Distance
* Unique Paths
* Unique Paths II
* Minimum Path Sum
* Partition Equal Subset Sum
* Target Sum
* Palindromic Substrings
* Longest Palindromic Subsequence

#### Final hedef

Karışık problem setlerinde problemi doğru kategoriye ayırabilmek.

---

# 7. Problem Pattern Listesi

## Array / String

* Prefix sum
* Sliding window
* Two pointers
* Frequency map
* Sorting
* In-place modification

## Stack

* Parentheses
* Monotonic stack
* Expression evaluation
* Undo behavior

## Queue

* BFS
* Streaming data
* Fixed-size recent events

## Linked List

* Fast/slow pointers
* Reversal
* Dummy node
* Merge
* Cycle detection

## Hashing

* Lookup
* Frequency counting
* Grouping
* Prefix sum + map

## Tree

* DFS recursion
* BFS level order
* Path tracking
* Subtree aggregation
* BST invariant

## Graph

* BFS shortest path in unweighted graph
* DFS connected components
* Topological sort
* Union-Find
* Dijkstra

## DP

* 1D DP
* 2D DP
* Knapsack
* Subsequence
* Grid DP
* Palindrome DP

---

# 8. Swift Implementasyon Projeleri

Her veri yapısı için ayrı dosya ve test yazılmalı.

## Paket yapısı önerisi

```text
DSA-Swift/
  Sources/
    DataStructures/
      Stack.swift
      Queue.swift
      Deque.swift
      LinkedList.swift
      HashMap.swift
      Heap.swift
      PriorityQueue.swift
      Trie.swift
      Graph.swift
      UnionFind.swift
    Algorithms/
      BinarySearch.swift
      Sorting.swift
      Recursion.swift
      Backtracking.swift
      GraphAlgorithms.swift
      DynamicProgramming.swift
  Tests/
    DataStructuresTests/
    AlgorithmsTests/
  Notes/
    BigO.md
    Patterns.md
    ProblemLog.md
```

## Yazılması gereken yapılar

1. Stack
2. Queue
3. CircularQueue
4. Deque
5. SinglyLinkedList
6. DoublyLinkedList
7. HashMap
8. HashSet
9. BinaryTree
10. BinarySearchTree
11. Heap
12. PriorityQueue
13. Trie
14. Graph
15. WeightedGraph
16. UnionFind
17. LRUCache
18. SegmentTree başlangıç seviyesi
19. FenwickTree başlangıç seviyesi

---

# 9. Swift Kod Standartları

Her implementasyon şu özellikleri taşımalı:

* Generic olmalı.
* Gereksiz force unwrap kullanılmamalı.
* Public API temiz olmalı.
* Complexity comment eklenmeli.
* Unit test yazılmalı.
* Edge case test edilmeli.

Örnek comment formatı:

```swift
/// Inserts an element into the heap.
/// Time: O(log n)
/// Space: O(1)
mutating func insert(_ value: Element) {
    storage.append(value)
    siftUp(from: storage.count - 1)
}
```

---

# 10. Haftalık Problem Sayısı Hedefi

Başlangıç seviyesi:

* 8-10 problem / hafta
* Çoğunlukla Easy
* Haftada 2 Medium

Orta seviye:

* 12-15 problem / hafta
* Easy + Medium dengeli
* Haftada 1 Hard analizi

İleri seviye:

* 15-25 problem / hafta
* Medium ağırlıklı
* Haftada 2-3 Hard denemesi

---

# 11. Tekrar Sistemi

Problem çözüldükten sonra tekrar tarihi verilmeli.

* 1. tekrar: 1 gün sonra
* 2. tekrar: 3 gün sonra
* 3. tekrar: 7 gün sonra
* 4. tekrar: 14 gün sonra
* 5. tekrar: 30 gün sonra

Her tekrar için hedef:

* Çözümü hatırlamak değil, kalıbı tekrar kurmak.
* Kodun tamamını yeniden yazmak.
* Complexity analizini tekrar yapmak.

---

# 12. Interview Simülasyonu

Her 4 haftada bir simülasyon yapılmalı.

## Simülasyon formatı

* 45 dakika süre.
* 1 Medium problem.
* İlk 5 dakika problem analizi.
* 25 dakika çözüm.
* 10 dakika test / refactor.
* 5 dakika complexity ve açıklama.

## Değerlendirme

```markdown
Problem:
Pattern:
Çözüm tamamlandı mı:
Brute force anlatıldı mı:
Optimize çözüm bulundu mu:
Time complexity:
Space complexity:
Edge case test edildi mi:
Swift kod kalitesi:
Eksikler:
```

---

# 13. Zorunlu Mini Projeler

## Proje 1: Custom Collections Package

Amaç: Swift Package içinde temel veri yapılarını yazmak.

İçerik:

* Stack
* Queue
* LinkedList
* BinarySearchTree
* Heap
* Trie
* Graph

## Proje 2: Autocomplete Engine

Kullanılan yapılar:

* Trie
* Dictionary
* PriorityQueue

Özellikler:

* Kelime ekleme
* Prefix arama
* En popüler sonuçları döndürme

## Proje 3: Route Finder

Kullanılan algoritmalar:

* Graph
* BFS
* Dijkstra

Özellikler:

* Şehir / nokta grafı
* En kısa yol
* Ağırlıklı yol hesaplama

## Proje 4: LRU Cache

Kullanılan yapılar:

* Dictionary
* DoublyLinkedList

Özellikler:

* O(1) get
* O(1) put
* Capacity eviction

## Proje 5: Problem Pattern Classifier

Amaç: Çözülen problemleri pattern'e göre sınıflandırmak.

Özellikler:

* Problem adı
* Pattern
* Difficulty
* Çözüm tarihi
* Tekrar tarihi
* Notlar

---

# 14. Gelişim Metrikleri

Aylık ölçülmesi gerekenler:

* Toplam çözülen problem sayısı
* Easy / Medium / Hard dağılımı
* Ortalama çözüm süresi
* Tekrar edilen problem sayısı
* Yardımsız çözülen problem oranı
* En zayıf 3 konu
* En güçlü 3 konu
* Swift implementasyon sayısı

## Hedef seviyeler

### Ay 1

* 40+ problem
* Stack, Queue, LinkedList implement edilmiş
* Big-O rahat okunuyor

### Ay 2

* 90+ toplam problem
* Hashing, sorting, binary search oturmuş
* Medium problemlere geçilmiş

### Ay 3

* 150+ toplam problem
* Tree ve graph temel problemleri çözülebiliyor

### Ay 4

* 220+ toplam problem
* DP temel problemleri çözülebiliyor
* Interview simülasyonu yapılabiliyor

### Ay 5-6

* 300+ problem
* Medium ağırlıklı çözüm
* Sistematik açıklama yeteneği
* Custom Swift DSA package tamamlanmış

---

# 15. Aylık Değerlendirme Formatı

```markdown
## Ay Özeti

### Çözülen problem sayısı
Easy:
Medium:
Hard:
Toplam:

### Implement edilen veri yapıları
-

### En iyi olduğum konular
-

### En zayıf olduğum konular
-

### Ortalama problem çözüm sürem
-

### Yardımsız çözüm oranım
-

### Gelecek ay odak konularım
-

### Silinmesi gereken alışkanlıklar
-

### Devam ettirilmesi gereken alışkanlıklar
-
```

---

# 16. Zorlandığında Kullanılacak Debug Checklist

Bir problemde takılınca sırayla şunları kontrol et:

1. Input küçük örnekle elle çözüldü mü?
2. Brute force çözüm yazıldı mı?
3. Constraintler okundu mu?
4. Sorting yardımcı olur mu?
5. HashMap gerekli mi?
6. Two pointers mümkün mü?
7. Sliding window olabilir mi?
8. Stack gerekiyor mu?
9. Problem graph gibi modellenebilir mi?
10. Recursion tree var mı?
11. Overlapping subproblem var mı?
12. State tanımı yapılabiliyor mu?
13. Edge case listelendi mi?
14. Kod mu yanlış, algoritma mı yanlış?
15. Çözümü 10 dakika açıklayabiliyor musun?

---

# 17. Konu Önceliklendirme

En yüksek getirili konular:

1. Array / String
2. HashMap / Set
3. Two Pointers
4. Sliding Window
5. Stack
6. Binary Search
7. Tree DFS/BFS
8. Graph BFS/DFS
9. Heap / PriorityQueue
10. Dynamic Programming

Interview ve genel problem çözme için en kritik patternler:

* HashMap
* Sliding Window
* Two Pointers
* DFS/BFS
* Binary Search
* DP
* Heap

---

# 18. Örnek Günlük Programlar

## 60 dakikalık gün

* 10 dk tekrar
* 20 dk konu
* 20 dk problem
* 10 dk not

## 90 dakikalık gün

* 10 dk tekrar
* 25 dk konu
* 25 dk implementasyon
* 25 dk problem
* 5 dk log

## 150 dakikalık gün

* 15 dk tekrar
* 35 dk konu
* 45 dk implementasyon
* 45 dk problem
* 10 dk log

---

# 19. Haftalık Örnek Akış

## Pazartesi

* Yeni konu öğren.
* Basit implementasyon yap.
* 1 Easy problem çöz.

## Salı

* Aynı konudan 2 problem çöz.
* Complexity notu çıkar.

## Çarşamba

* Veri yapısını sıfırdan tekrar yaz.
* 1 Medium problem çöz.

## Perşembe

* Pattern odaklı problem çöz.
* Önceki problemleri tekrar et.

## Cuma

* Mini proje / refactor günü.

## Cumartesi

* 2-4 problem çöz.
* Haftalık eksikleri kapat.

## Pazar

* Hafif tekrar.
* Haftalık değerlendirme.
* Sonraki hafta planı.

---

# 20. Swift için Özel Dikkat Edilecek Noktalar

## String

Swift string Unicode-aware olduğu için indexleme maliyetlidir. LeetCode string problemlerinde çoğu zaman şu dönüşüm pratik olur:

```swift
let chars = Array(s)
```

Ama bunun O(n) zaman ve O(n) alan maliyeti vardır.

## Array slicing

`ArraySlice` bazen beklenmeyen memory retention yaratabilir. Büyük array üzerinde slice aldıktan sonra uzun süre tutmak gerekiyorsa yeni Array oluşturmak daha doğru olabilir.

## Mutating struct methods

Veri yapıları `struct` ise değiştirici metotlar `mutating` olmalı.

## Reference node structures

LinkedList, Tree, Graph node yapılarında `class` kullanımı çoğu zaman daha pratiktir.

## Comparable closure

Heap gibi yapılarda `areSorted: (Element, Element) -> Bool` closure'ı ile min/max heap aynı yapıdan üretilebilir.

---

# 21. Örnek Swift Data Structure API Tasarımları

## Stack API

```swift
struct Stack<Element> {
    var isEmpty: Bool
    var count: Int
    mutating func push(_ element: Element)
    mutating func pop() -> Element?
    func peek() -> Element?
}
```

## Queue API

```swift
struct Queue<Element> {
    var isEmpty: Bool
    var count: Int
    mutating func enqueue(_ element: Element)
    mutating func dequeue() -> Element?
    func peek() -> Element?
}
```

## Heap API

```swift
struct Heap<Element> {
    init(sort: @escaping (Element, Element) -> Bool)
    var isEmpty: Bool
    var count: Int
    mutating func insert(_ element: Element)
    mutating func remove() -> Element?
    func peek() -> Element?
}
```

## Trie API

```swift
final class TrieNode {
    var children: [Character: TrieNode]
    var isWord: Bool
}

final class Trie {
    func insert(_ word: String)
    func search(_ word: String) -> Bool
    func startsWith(_ prefix: String) -> Bool
}
```

## UnionFind API

```swift
struct UnionFind {
    mutating func find(_ x: Int) -> Int
    mutating func union(_ a: Int, _ b: Int)
    mutating func connected(_ a: Int, _ b: Int) -> Bool
}
```

---

# 22. Problem Seçim Stratejisi

Her konu için problem sırası:

1. Aynı pattern'den 2 Easy.
2. Aynı pattern'den 2 Medium.
3. Karışık 1 problem.
4. 3 gün sonra tekrar.
5. 1 hafta sonra farklı varyasyon.

Yanlış strateji:

* Rastgele problem seçmek.
* Çözümü hemen açmak.
* Sadece kod yazıp analiz yapmamak.
* Aynı problemi bir daha çözmemek.

Doğru strateji:

* Pattern bazlı ilerlemek.
* Önce brute force düşünmek.
* Optimize çözümü açıklamak.
* Not almak.
* Tekrar etmek.

---

# 23. Yardım Almadan Önce Bekleme Kuralları

Bir problemde takılınca:

* İlk 10 dk: sadece örnek çöz.
* Sonraki 10 dk: brute force yaz.
* Sonraki 10 dk: pattern seçmeye çalış.
* 30 dk sonunda hâlâ ilerleme yoksa sadece ipucu al.
* Çözümü tamamen okursan aynı problemi 24 saat içinde yeniden çöz.

---

# 24. Kod İnceleme Checklist

Her çözümden sonra sor:

1. Kod tüm edge caseleri kapsıyor mu?
2. Force unwrap var mı?
3. Gereksiz array copy var mı?
4. `removeFirst()` gibi maliyetli operasyon var mı?
5. String index maliyeti doğru hesaba katıldı mı?
6. Complexity doğru yazıldı mı?
7. Daha temiz API mümkün mü?
8. Testler yeterli mi?
9. Çözüm başka pattern ile daha iyi olur mu?
10. Açıklama interview ortamında anlaşılır mı?

---

# 25. İlk 14 Gün Detaylı Başlangıç Planı

## Gün 1

* Big-O temel kavramları.
* Swift Array traversal.
* 2 basit problem.

## Gün 2

* Space complexity.
* Nested loop analizi.
* Prefix sum giriş.

## Gün 3

* Swift Dictionary ve Set.
* Two Sum.
* Contains Duplicate.

## Gün 4

* String ve Character.
* Valid Anagram.
* First Unique Character.

## Gün 5

* Binary search mantığı.
* Binary Search.
* Search Insert Position.

## Gün 6

* Haftalık tekrar.
* Önceki 5 problem tekrar.

## Gün 7

* Hafif gün.
* Notları düzenle.
* Haftalık değerlendirme.

## Gün 8

* Two pointers.
* Valid Palindrome.
* Two Sum II.

## Gün 9

* In-place array update.
* Move Zeroes.
* Remove Duplicates from Sorted Array.

## Gün 10

* Sliding window fixed-size.
* Maximum Average Subarray.

## Gün 11

* Sliding window variable-size.
* Longest Substring Without Repeating Characters.

## Gün 12

* Prefix sum + HashMap.
* Subarray Sum Equals K.

## Gün 13

* Karma problem günü.
* 3 problem.

## Gün 14

* Haftalık değerlendirme.
* Yanlış çözülen problemleri yeniden çöz.

---

# 26. Final Kontrol Listesi

Program sonunda şunları yapabiliyor olmalısın:

* Bir problemi 5 dakika içinde doğru kategoriye koymak.
* Brute force ve optimize çözümü açıklamak.
* Swift ile temiz, güvenli ve test edilebilir çözüm yazmak.
* Karmaşıklık analizini doğru yapmak.
* Tree / Graph / DP problemlerinden kaçmamak.
* Custom data structure implementasyonlarını sıfırdan yazmak.
* Interview formatında düşünce sürecini anlatmak.

---

# 27. Günlük Komut Formatı

Her gün çalışmaya başlarken şu format kullanılabilir:

```markdown
Bugün roadmap'te kaldığım yer: Hafta X / Gün Y.
Dünkü logum:
-
Bugün için 90 dakikam var.
Bana bugünün konu, implementasyon ve problem listesini çıkar.
```

Gün sonunda:

```markdown
Bugünkü çalışmalarım:
-
Çözdüğüm problemler:
-
Takıldığım noktalar:
-
Bana günlük puanımı ver ve yarınki planı çıkar.
```

Bu formatla günlük takip sürdürülebilir hale gelir.
