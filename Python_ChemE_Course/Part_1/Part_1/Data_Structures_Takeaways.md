# 📘 Data Structures in Python: Key Takeaways

---

### ***Python Data Structures and functions: Key takeaways for revision*** 
***15/09/2025***

#### *Introduction*
This document summarizes key takeways from a set of 20 python exercises ( *15 basic and 5 project-based* ) focusing on data structures ( *Lists, Tuples, sets and dictionanires* ) and *functions*. It is designed for revision and to guide solving future problems by highlighting essential concepts, techniques, and best practices. Each section covers a data structure or category, with explanation, code examples and tips for practical application.

#### 1. *Lists*
Lists are mutable, ordered collections. Key lessons from exercises include efficient manipulation, avoiding built-in methods for learning and handling edge cases. 

##### ***Key takeaways***
- **Reversing a List**: Use a loop to revers a list manually, iterating from the end to create a new list. This reinforces indexing and iteration.
- **Removing Duplicates**: Preserve ordre using a dictionary or list to track seen elements. Dictionaries are faster for large lists ((O1) lookup).
- **finding second Largest**: Track largest and second largest in one pass to avoid soring (O(n) *vs* O(n log(n))).
- **Edge Cases**: Handle empty lists, single-element lists, and duplicates explicitly. 

##### ***Example: Remove Duplicates***: 
    def remove_duplicates(lst):
        seen= []
        for item in lst:
            if item not in seen : 
                seen.append(item)
        return seen


*Tip*: Use a set for O(n) time complexity if order doesn't matter:  *return list(dict.fromkeys( lst) ).*

#### 2. *Tuples* 
Tuples are immutable, ordered collections, ideal for fixed data.
##### ***Key takeaways***
- ***Counting Elements***: use *tuple.count()* for simplicity or a loop for explicit control. 
- ***Merging and sorting***: Convert tuples to lists for manipulation, then back to typles. Use *Sorted()* for efficient sorting.
- ***Edge Cases***: Handle empty tuples and non-existent elements. Ensure immutability is respected by creating new tuples.

##### ***Example: Merge and sort Tuples*** 
    def merge_and_sort(tup1,tup2):
        merged= list(tup1)+list(tup2)
        return tuple(sorted(merged))

*Tip* For unique elements, use *set()* before sorting: *tuple(sorted(set(tup1) set(tup2)))*

#### 3. *Sets*
Set are unordered, mutable collections of unique, hashable elements. 

##### ***Key Takeaways*** 
- ***Finding Common Elements***: Use *intersection()* *or* *&* for O(min(n,m)) complexity where n and m are set sizes.
- ***Removing Elements***: Use *discard()* to safely remove elemnts without errors for non-exisitent items, unlike *remove()*.
- ***Efficiency***: Set offer O(1) average-case lookup and modification, ideal for membership testing and deduplication.
- ***Edge Cases***: Handle empty sets and unhashable elements (e.g., lists) by raising appropriate errors
##### ***Example: Remove Elements from set***
    def remove_from_set(s,lst):
        s.difference_update(lst)
        return s

*Tip*: Use *copy()* to preserve the original set: *s.copy().difference_update(lst)*

#### 4. *Dictionaries*
Dictionaries are mutable, key-value mappings with fast lookup (O(1) average)
##### ***Key Takeaways***
- ***Counting Frequencies***: Use a dictionary or *collections.Counter* to count occurences. *Counter* is optimized for this task
- ***Merging Dictionaries***: Sum values for common keys using a loop or *dict.get(key,0)*. The | Operator merges but dosen't sum values.
- ***Inverting Dictionaries***: Ensure values are unique and hashable. Use a loop to swap key and values
- ***Edge Cases***: Handle empty dictionaries, non-numeric values, and duplicate keys (last value wins).

##### ***Example: Count word Frequencies***
    def word_frequencies(text):
        if no text:
            return{}
        words= text.lower().split()
        freq={}
        for word in words: 
            freq[word]=freq.get(word,0) + 1
        return freq


*Tip*: For cleaner code, use *from collections import Counter*.
*dict(Counter(words))*

#### 5. *Function*
Functions encapsulate logic, supporting recirsion, comprehensions, and higher-order functions.

##### ***Key Takeaways***
- ***Recursion***: Define clear base cases (e.g., factorial for n=0 or 1) to avoid infinite recursion.
- ***List Comprhensions***: Use for concise filtering (e.g, even numbers). Ensure readability over complexity.
- ***Default/Keyword Arguments***: Use for flexibility (e.g., tax rate defaults). Validate inputs to avoid errors.
- ***Higher-Order Functions***: Pass functions as arguments to apply transformations (e.g., squaring a list).
- ***Edge Cases***: Handle invlaid inputs (e.g., negative numbers, empty lists) with explicit checks.

##### ***Example: Filter Even numbers***
    def filter_even_numbers(lst):
        return [x for x in lst if x % 2 ==0]

*Tip* Use *filter()* with a lambda for an alternative:         
        *list(filter(lambda x : x % 2 ==0, lst))*

---

#### 6. *Project Exercises: Real-World Applications*
Project exercises combine multiple data structures for complex tasks.
##### 1. *Inventory Management System*
*Takeaway*: Use dictionaries for inventory, lists for results and tuples for operations. Validate inputs and handle non-existent items.
*Example*



```python
def manage_inventory(operations):
    inventory = {} # Dictionary to hold item quantities
    check_results = [] # To store results of 'check' operations
    for item, action, quantity in operations:
        if not isinstance(quantity,(int,float)) or quantity < 0:
            raise ValueError("Invalid quantity")
        inventory.setdefault(item, 0) # Initialize if not present
        if action == 'add':
            inventory[item] += quantity
        elif action == 'remove':
            inventory[item] = max(0, inventory[item] - quantity)
        elif action == 'check':
            check_results.append((item, inventory[item]))
    return inventory, check_results

    
```

*Tip* Use *Collections.defaultdict(int)* to simplify initialization
#### 2. *Unique Word Pairs*
*Takaway*: Use sets for unique pars, tuples for word pairs, and string preprocessing for case-insensitivity. Handle edge cases with fewer than two words. 
**Example:**



```python
def unique_word_pairs(text):
    words=text.lower().split()
    if len(words)<2:
        return set()
    return { (words[i], words[i+1]) for i in range(len(words) -1 ) }# Set comprehension for unique pairs

```

*Tip*: Use *re.findall(r'\w+', text.lower())* to ingore punctuation.
#### 3. *Student grade Analyser*
*Takeaway* : Combine lists, tuples and dictionaries. Use helper function for modularity and validate inputs rigorously. 
**Example**: 



```python
def student_grade_analyzer(students):
    # Helper function to validate student data
    def validate_student(student):
        if (not isinstance(student, tuple) or len(student) != 3 or # Ensure it's a tuple of length 3
            not isinstance(student[0], str) or # Name should be a string
            not isinstance(student[1], int) or not (0 <= student[1] <= 100) or # Midterm should be int 0-100
            not isinstance(student[2], int) or not (0 <= student[2] <= 100)): # Final should be int 0-100
            raise ValueError("Invalid student data")
    
    grade_distribution = {'A': 0, 'B': 0, 'C': 0, 'D': 0, 'F': 0}
    student_averages = {}
    
    for student in students:
        validate_student(student)
        name, midterm, final = student
        average = (midterm + final) / 2
        student_averages[name] = average
        
        if average >= 90:
            grade_distribution['A'] += 1
        elif average >= 80:
            grade_distribution['B'] += 1
        elif average >= 70:
            grade_distribution['C'] += 1
        elif average >= 60:
            grade_distribution['D'] += 1
        else:
            grade_distribution['F'] += 1
    
    return student_averages, grade_distribution
```


```python
def studen_grade(student):
    if not students:
        return {}
    def get_grade_and_status(avg):
        if avg >= 90:
            return 'A', 'True'
        elif avg >= 80:
            return 'B', 'True'
        elif avg >= 70:
            return 'C', 'Trues'
        elif avg >= 60:
            return 'D', 'True'
        else:
            return 'F', 'False'
    result= {}
    for name, scores in student:
        if no isinstance(name,str) or not name.strip():
            raise ValueError("Invalid name")
        if not scores: 
            raise ValueError("Scores list cannot be empty")
        if any(not isinstance(score,(int,float)) or not (0 <= score <= 100) for score in scores):
            raise ValueError("Invalid score in scores list")
        avg=sum(scores)/len(scores)
        grade, passed=get_grade_and_status(avg)
        result[name]={round(avg,2),grade,passed}
    return result
```

*Tip*: Use a dictionary for grade ranges to make thresholds configurable.



---

✅ *This document is an enhanced export from the original Jupyter Notebook for easier review and study.*
