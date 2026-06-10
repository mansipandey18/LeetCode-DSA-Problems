# <u>1268. Search Suggestions System</u>

----

## 🔗 Problem Link
https://leetcode.com/problems/search-suggestions-system/

---

## 🧠 Intuition:
* 🔹 Sort the `products` array first so that products are stored in **lexicographical order**.

* 🔹 Build a **Trie** where each node represents a prefix of product names.

* 🔹 While inserting a product into the Trie, store its index at every visited node.

* 🔹 Keep only the **first 3 indices** at each node since we only need the top 3 suggestions.

* 🔹 Because products are inserted after sorting, the stored indices automatically correspond to the **3 smallest lexicographical products** for that prefix.

* 🔹 For the `searchWord`, traverse the Trie character by character.

* 🔹 At each prefix, retrieve the stored product indices from the current Trie node.

* 🔹 If a prefix is not found, all remaining prefixes will have empty suggestion lists.

* 🔹 Convert the stored indices back into product names and return the suggestions for each prefix.

---

## ⏱ Time Complexity

**O(n log n + Σ|product| + m)**

* Sorting products: `O(n log n)`
* Building Trie: `O(Σ|product|)`
* Searching prefixes of searchWord: `O(m)`
* Converting indices to product names: `O(3m) ≈ O(m)`
    
---

## 📦 Space Complexity

**O(Σ|product|)**

* Trie stores all characters of all products: `O(Σ|product|)`
* Each Trie node stores at most 3 indices (constant extra space per node).

---

## 💻 Java Code

```java
class Trie {
    Trie[] children = new Trie[26];
    List<Integer> productIndices = new ArrayList<>();

    public void insert(String word, int index) {
        Trie currentNode = this;
      
        for (int i = 0; i < word.length(); i++) {
            int charIndex = word.charAt(i) - 'a';
          
            if (currentNode.children[charIndex] == null) {
                currentNode.children[charIndex] = new Trie();
            }
          
            currentNode = currentNode.children[charIndex];
          
            if (currentNode.productIndices.size() < 3) {
                currentNode.productIndices.add(index);
            }
        }
    }

    public List<Integer>[] search(String searchWord) {
        Trie currentNode = this;
        int wordLength = searchWord.length();
      
        List<Integer>[] results = new List[wordLength];
        Arrays.setAll(results, i -> new ArrayList<>());
      
        for (int i = 0; i < wordLength; i++) {
            int charIndex = searchWord.charAt(i) - 'a';
          
            if (currentNode.children[charIndex] == null) {
                break;
            }
          
            currentNode = currentNode.children[charIndex];
            results[i] = currentNode.productIndices;
        }
      
        return results;
    }
}
class Solution {
    public List<List<String>> suggestedProducts(String[] products, String searchWord) {
        Arrays.sort(products);
      
        
        Trie trie = new Trie();
        for (int i = 0; i < products.length; i++) {
            trie.insert(products[i], i);
        }
      
        List<Integer>[] productIndicesArray = trie.search(searchWord);
      
        List<List<String>> suggestions = new ArrayList<>();
        for (List<Integer> indices : productIndicesArray) {
            List<String> productNames = new ArrayList<>();
            for (int productIndex : indices) {
                productNames.add(products[productIndex]);
            }
            suggestions.add(productNames);
        }
      
        return suggestions;
    }
}
```

---