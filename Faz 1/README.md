# Big-O, Swift Temelleri ve Problem Çözme Disiplini

## 1. Time Complexity

**Time complexity**, input büyüdükçe algoritmanın çalışma süresinin nasıl arttığını ifade eder.

Önemli nokta:
Big-O gerçek süreyi değil, **büyüme oranını** anlatır.

```swift
func printAll(_ numbers: [Int]) {
    for number in numbers {
        print(number)
    }
}
```

Burada `n` eleman varsa döngü `n` kez çalışır.

```text
Time: O(n)
```

---

## 2. Space Complexity

**Space complexity**, algoritmanın input dışında ne kadar ek bellek kullandığını ifade eder.

```swift
func sum(_ numbers: [Int]) -> Int {
    var total = 0

    for number in numbers {
        total += number
    }

    return total
}
```

Burada sadece `total` değişkeni kullanılır.

```text
Space: O(1)
```

Ama aşağıdaki örnekte yeni bir array oluşturulur:

```swift
func doubled(_ numbers: [Int]) -> [Int] {
    var result: [Int] = []

    for number in numbers {
        result.append(number * 2)
    }

    return result
}
```

```text
Space: O(n)
```

---

## 3. Big-O, Big-Theta, Big-Omega

### Big-O — Upper Bound

En kötü durumda algoritmanın ne kadar büyüyebileceğini ifade eder.

```text
O(n)
```

“En fazla lineer büyür” anlamına gelir.

---

### Big-Theta — Tight Bound

Algoritmanın gerçek büyüme sınıfını ifade eder.

```text
Θ(n)
```

“Ne eksik ne fazla, lineer büyür” anlamına gelir.

---

### Big-Omega — Lower Bound

En iyi durumda algoritmanın en az ne kadar çalışacağını ifade eder.

```text
Ω(1)
```

“En iyi durumda sabit zamanda bitebilir” anlamına gelir.

---

## 4. Best / Average / Worst Case

Örnek: Array içinde eleman arama.

```swift
func contains(_ target: Int, in numbers: [Int]) -> Bool {
    for number in numbers {
        if number == target {
            return true
        }
    }

    return false
}
```

| Durum        | Açıklama              | Complexity |
| ------------ | --------------------- | ---------- |
| Best case    | Eleman ilk sırada     | O(1)       |
| Average case | Eleman ortalarda      | O(n)       |
| Worst case   | Eleman yok veya sonda | O(n)       |

---

## 5. Yaygın Karmaşıklıklar

| Complexity | İsim         | Örnek                     |
| ---------- | ------------ | ------------------------- |
| O(1)       | Constant     | Array index access        |
| O(log n)   | Logarithmic  | Binary search             |
| O(n)       | Linear       | Array traversal           |
| O(n log n) | Linearithmic | Efficient sorting         |
| O(n²)      | Quadratic    | Nested loop               |
| O(2ⁿ)      | Exponential  | Naive recursive Fibonacci |

---

## 6. Constant — O(1)

Input büyüse bile işlem sayısı değişmez.

```swift
func firstElement(_ numbers: [Int]) -> Int? {
    numbers.first
}
```

```text
Time: O(1)
Space: O(1)
```

---

## 7. Logarithmic — O(log n)

Her adımda problem yarıya iner.

```swift
func binarySearch(_ numbers: [Int], target: Int) -> Int? {
    var left = 0
    var right = numbers.count - 1

    while left <= right {
        let mid = left + (right - left) / 2

        if numbers[mid] == target {
            return mid
        } else if numbers[mid] < target {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }

    return nil
}
```

```text
Time: O(log n)
Space: O(1)
```

Not: Binary search sadece **sorted array** üzerinde çalışır.

---

## 8. Linear — O(n)

Input kadar işlem yapılır.

```swift
func maxValue(_ numbers: [Int]) -> Int? {
    guard var max = numbers.first else { return nil }

    for number in numbers {
        if number > max {
            max = number
        }
    }

    return max
}
```

```text
Time: O(n)
Space: O(1)
```

---

## 9. Linearithmic — O(n log n)

Genellikle verimli sıralama algoritmalarında görülür.

Swift’in `sorted()` fonksiyonu pratikte karşılaştırmalı sıralama yaptığı için tipik analizde:

```swift
let sortedNumbers = numbers.sorted()
```

```text
Time: O(n log n)
Space: implementation-dependent
```

---

## 10. Quadratic — O(n²)

Nested loop varsa çoğu zaman O(n²) olur.

```swift
func printPairs(_ numbers: [Int]) {
    for i in numbers {
        for j in numbers {
            print(i, j)
        }
    }
}
```

`n` eleman varsa:

```text
n * n = n²
Time: O(n²)
Space: O(1)
```

---

## 11. Exponential — O(2ⁿ)

Naive recursive Fibonacci klasik örnektir.

```swift
func fibonacci(_ n: Int) -> Int {
    if n <= 1 { return n }

    return fibonacci(n - 1) + fibonacci(n - 2)
}
```

```text
Time: O(2ⁿ)
Space: O(n)
```

Buradaki `Space: O(n)` recursion call stack yüzündendir.

---

# Swift Collection Complexity

Swift’in temel koleksiyon tipleri `Array`, `Set` ve `Dictionary`’dir. Swift dokümantasyonu da bu üç koleksiyonu ana collection type olarak tanımlar. ([Swift Belgeleri][1])

## 12. Swift Array Complexity

Array sıralı veri tutar. Index ile erişim çok hızlıdır.

| Operation       | Ortalama Complexity | Not                              |
| --------------- | ------------------: | -------------------------------- |
| `array[index]`  |                O(1) | Random access                    |
| `append`        |      Amortized O(1) | Kapasite dolarsa resize olabilir |
| `insert(at: 0)` |                O(n) | Elemanlar kaydırılır             |
| `removeLast()`  |                O(1) | Son eleman silinir               |
| `remove(at:)`   |                O(n) | Elemanlar kaydırılır             |
| `contains`      |                O(n) | Linear search                    |
| Traversal       |                O(n) | Tüm elemanlar gezilir            |

Apple’ın `Set` dokümantasyonu, üyelik testi önemliyse ve sıralama gerekmiyorsa `Array` yerine `Set` kullanılmasını önerir; bu da `Array.contains` gibi lineer aramaların büyük veri için maliyetli olabileceği pratik durumlara işaret eder. ([Apple Developer][2])

---

## 13. Swift Dictionary Complexity

Dictionary key-value veri tutar.

```swift
var ages: [String: Int] = [
    "Ali": 30,
    "Ayşe": 25
]

let age = ages["Ali"]
```

| Operation         | Ortalama Complexity |
| ----------------- | ------------------: |
| Lookup by key     |                O(1) |
| Insert / update   |                O(1) |
| Remove by key     |                O(1) |
| Iterate all pairs |                O(n) |

Not: Dictionary hash table tabanlıdır. Ortalama O(1) beklenir, ama hash collision gibi durumlarda worst-case daha kötü olabilir.

---

## 14. Swift Set Complexity

Set benzersiz elemanlar tutar.

```swift
var ids: Set<Int> = [1, 2, 3]

ids.contains(2)
```

| Operation          | Ortalama Complexity |
| ------------------ | ------------------: |
| `contains`         |                O(1) |
| `insert`           |                O(1) |
| `remove`           |                O(1) |
| Iterate all values |                O(n) |

`Set`, üyelik testi için verimlidir ve eleman sırası önemli olmadığında `Array` yerine tercih edilebilir. ([Apple Developer][2])

---

# Mutability

## 15. `let` vs `var`

Swift’te mutability `let` ve `var` ile kontrol edilir.

```swift
let name = "Omer"
// name = "Ali" // Hata

var age = 30
age = 31 // Geçerli
```

| Keyword | Anlam     |
| ------- | --------- |
| `let`   | Immutable |
| `var`   | Mutable   |

---

## 16. Collection Mutability

```swift
let numbers = [1, 2, 3]
// numbers.append(4) // Hata

var mutableNumbers = [1, 2, 3]
mutableNumbers.append(4)
```

Array, Dictionary ve Set `let` ile tanımlanırsa koleksiyonun içeriği değiştirilemez.

---

# Value vs Reference Types

## 17. Value Type

`struct`, `enum`, `Array`, `Dictionary`, `Set` value type’tır.

```swift
var a = [1, 2, 3]
var b = a

b.append(4)

print(a) // [1, 2, 3]
print(b) // [1, 2, 3, 4]
```

`b`, `a`’dan bağımsız davranır.

Swift koleksiyonları value semantics sunar; ancak performans için copy-on-write optimizasyonu kullanırlar.

---

## 18. Reference Type

`class` reference type’tır.

```swift
final class User {
    var name: String

    init(name: String) {
        self.name = name
    }
}

let user1 = User(name: "Omer")
let user2 = user1

user2.name = "Ali"

print(user1.name) // Ali
print(user2.name) // Ali
```

İki değişken aynı instance’ı referans eder.

---

# Problem Çözme Disiplini

## 19. Analiz Sırası

Bir algoritma sorusunda şu sırayı kullan:

```text
1. Input nedir?
2. Output nedir?
3. Constraint var mı?
4. Sorted mı?
5. Duplicate olabilir mi?
6. Negative değer olabilir mi?
7. Boş input olabilir mi?
8. Brute force çözüm nedir?
9. Daha iyi veri yapısı var mı?
10. Time / space complexity nedir?
```

---

## 20. Brute Force Önce Yazılır

Örnek: Two Sum.

```swift
func twoSumBruteForce(_ numbers: [Int], target: Int) -> (Int, Int)? {
    for i in 0..<numbers.count {
        for j in i + 1..<numbers.count {
            if numbers[i] + numbers[j] == target {
                return (i, j)
            }
        }
    }

    return nil
}
```

```text
Time: O(n²)
Space: O(1)
```

---

## 21. Dictionary ile Optimize Etme

```swift
func twoSum(_ numbers: [Int], target: Int) -> (Int, Int)? {
    var seen: [Int: Int] = [:]

    for i in 0..<numbers.count {
        let current = numbers[i]
        let complement = target - current

        if let previousIndex = seen[complement] {
            return (previousIndex, i)
        }

        seen[current] = i
    }

    return nil
}
```

```text
Time: O(n)
Space: O(n)
```

Burada zaman kazanmak için ek bellek kullanılır.

---

# Implementasyonlar

## 22. Basit Benchmark Helper

```swift
import Foundation

@discardableResult
func benchmark<T>(
    _ title: String,
    operation: () -> T
) -> T {
    let start = CFAbsoluteTimeGetCurrent()
    let result = operation()
    let end = CFAbsoluteTimeGetCurrent()

    let elapsed = end - start
    print("\(title): \(elapsed) seconds")

    return result
}
```

Kullanım:

```swift
let numbers = Array(0..<1_000_000)

benchmark("Array traversal") {
    var total = 0

    for number in numbers {
        total += number
    }

    return total
}
```

Not: Microbenchmark sonuçları cihaz, build configuration, optimizer, debug/release farkı ve runtime koşullarından etkilenir. Algoritmik analiz için Big-O esas alınmalıdır.

---

## 23. Array Traversal Örnekleri

### Tüm elemanları gezme

```swift
func printNumbers(_ numbers: [Int]) {
    for number in numbers {
        print(number)
    }
}
```

```text
Time: O(n)
Space: O(1)
```

---

### Toplam alma

```swift
func sum(_ numbers: [Int]) -> Int {
    var total = 0

    for number in numbers {
        total += number
    }

    return total
}
```

```text
Time: O(n)
Space: O(1)
```

---

### Yeni array üretme

```swift
func squared(_ numbers: [Int]) -> [Int] {
    var result: [Int] = []
    result.reserveCapacity(numbers.count)

    for number in numbers {
        result.append(number * number)
    }

    return result
}
```

```text
Time: O(n)
Space: O(n)
```

`reserveCapacity` zorunlu değildir ama append sırasında tekrar tekrar kapasite artırma ihtimalini azaltır.

---

## 24. Nested Loop Analizleri

### Bağımsız nested loop

```swift
func allPairs(_ numbers: [Int]) {
    for i in 0..<numbers.count {
        for j in 0..<numbers.count {
            print(numbers[i], numbers[j])
        }
    }
}
```

```text
n * n = n²
Time: O(n²)
Space: O(1)
```

---

### Üçgen nested loop

```swift
func uniquePairs(_ numbers: [Int]) {
    for i in 0..<numbers.count {
        for j in i + 1..<numbers.count {
            print(numbers[i], numbers[j])
        }
    }
}
```

Çalışma sayısı yaklaşık:

```text
n(n - 1) / 2
```

Big-O’da sabitler atılır:

```text
Time: O(n²)
Space: O(1)
```

---

### İç döngü sabitse

```swift
func printFirstTenForEach(_ numbers: [Int]) {
    for number in numbers {
        for i in 0..<10 {
            print(number, i)
        }
    }
}
```

```text
n * 10 = 10n
Time: O(n)
Space: O(1)
```

---

## 25. Binary Search Helper

Generic ve reusable bir binary search helper:

```swift
func binarySearch<T: Comparable>(
    in array: [T],
    target: T
) -> Int? {
    var left = 0
    var right = array.count - 1

    while left <= right {
        let mid = left + (right - left) / 2
        let value = array[mid]

        if value == target {
            return mid
        } else if value < target {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }

    return nil
}
```

Kullanım:

```swift
let numbers = [1, 3, 5, 7, 9, 11]

let index = binarySearch(in: numbers, target: 7)

print(index as Any) // Optional(3)
```

```text
Time: O(log n)
Space: O(1)
```

---

## 26. Binary Search Edge Case

Boş array için yukarıdaki implementation problem yaratabilir:

```swift
var right = array.count - 1
```

`array.count == 0` olduğunda `right = -1` olur. `Int` açısından çalışabilir ama daha güvenli hali:

```swift
func safeBinarySearch<T: Comparable>(
    in array: [T],
    target: T
) -> Int? {
    guard !array.isEmpty else { return nil }

    var left = 0
    var right = array.count - 1

    while left <= right {
        let mid = left + (right - left) / 2
        let value = array[mid]

        if value == target {
            return mid
        } else if value < target {
            left = mid + 1
        } else {
            right = mid - 1
        }
    }

    return nil
}
```

---

# Kısa Ezber Tablosu

| Yapı / İşlem           |     Complexity |
| ---------------------- | -------------: |
| Array index access     |           O(1) |
| Array traversal        |           O(n) |
| Array search           |           O(n) |
| Array insert beginning |           O(n) |
| Array append           | Amortized O(1) |
| Dictionary lookup      |   Average O(1) |
| Dictionary insert      |   Average O(1) |
| Set contains           |   Average O(1) |
| Binary search          |       O(log n) |
| Nested loop            |          O(n²) |
| Sorting                |     O(n log n) |

---

# Mülakat Cevap Şablonu

Bir çözümü anlatırken şu format yeterlidir:

```text
Önce brute force çözüm O(n²) olur.
Her eleman için diğer elemanları kontrol ederim.

Daha iyi çözümde Dictionary kullanırım.
Daha önce gördüğüm değerleri key olarak saklarım.
Her eleman için complement’i O(1) average lookup ile kontrol ederim.

Time complexity: O(n)
Space complexity: O(n)
```

Swift karşılığı:

```swift
func solve(_ numbers: [Int], target: Int) -> (Int, Int)? {
    var seen: [Int: Int] = [:]

    for index in numbers.indices {
        let value = numbers[index]
        let complement = target - value

        if let previousIndex = seen[complement] {
            return (previousIndex, index)
        }

        seen[value] = index
    }

    return nil
}
```

[1]: https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes/?utm_source=chatgpt.com "Collection Types - Documentation"
[2]: https://developer.apple.com/documentation/swift/set?utm_source=chatgpt.com "Set | Apple Developer Documentation"
