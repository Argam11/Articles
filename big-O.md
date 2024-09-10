# Big O Notation

## Big O(log N) Logarithmic complexity

![Alt text](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20220812122843/Logarithmic-time-complexity-blog-1.jpg "a title")

**In a logarithmic time complexity**, as the input size increases, the time required to perform the algorithm’s operations increases at a rate proportional to the logarithm of the input size. This is considered very efficient compared to linear (O(N)), quadratic (O(N^2)), or cubic (O(N^3)) time complexities, especially for large input sizes.

One of the known examples of an algorithm with O(log N) complexity is the Binary Search Algorithm.

```
function binarySearch(arr, target) {
  let start = 0;
  let end = arr.length - 1;

  while (start <= end) {
    let middle = Math.floor((end - start) / 2) + start;

    if (arr[middle] < target) {
      // Search the right half
      start = middle + 1;
    } else if (arr[middle] > target) {
      // Search the left half
      end = middle - 1;
    } else if (arr[middle] === target) {
      // Found target
      return middle;
    }
  }

  // Target not found
  return -1
}

console.log(binarySearch([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32], 31));
```

### 32 elements = 5 “steps” at worst case.

![Alt text](https://www.doabledanny.com/static/c42dbf1ed557c9c70320b7f61c577df7/2.png "a title")

In Big O notation, `O(log n)` typically refers to logarithmic complexity, and regardless of the base, the difference between bases is just a constant factor, which doesn't change the overall complexity class. Thus, `O(log_2 n)` is considered the same as `O(log n)`.
To get a sense of how logarithmic complexity scales, let's calculate log ⁡𝑛 for input sizes of 1 million and 1 billion.

log_2 1.000.000 ≈ 19.93;

log_2 1.000.000.000 ≈ 29.88;

Now we can consider Binary Search with `O(log_3 n)`

### 32 elements = 3 “steps” at worst case with `O(log_3 n)`.

```
function binarySearch(arr, target) {
  let start = 0;
  let end = arr.length - 1;

  while (start <= end) {
    let middle1 = Math.floor((end - start) / 3) + start;
    let middle2 = Math.floor((end - start) / 3) * 2 + start;

    if (arr[middle1] < target) {
      // Search the right half
      start = middle1 + 1;
    } else if (arr[middle1] > target) {
      // Search the left half
      end = middle1 - 1;
    } else if (arr[middle1] === target) {
      // Found target
      return middle1;
    }

    if (arr[middle2] < target) {
      // Search the right half
      start = middle2 + 1;
    } else if (arr[middle2] > target) {
      // Search the left half
      end = middle2 - 1;
    } else if (arr[middle2] === target) {
      // Found target
      return middle2;
    }
  }

  // Target not found
  return -1;
}

console.log(binarySearch([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32], 31));
```

### Space complexity of Binary Search

Binary Search requires three pointers to elements (start, middle and end), regardless of the size of the array. Therefore the space complexity of Binary Search is O(1) – constant space.

### Performance summary table

![Alt text](https://www.doabledanny.com/static/91fbf40689fbdf195daefe5137621948/a9693/3.png "a title")

<br />

## Big O(n log(n)) Linearithmic time complexity

![Alt text](https://miro.medium.com/v2/resize:fit:1358/1*dWet_YU-5072Kcko7LzsuQ.jpeg "a title")

Linearithmic time is simply a combination of linear time `n` and logarithmic time `O(log n)`.

`n * log(n) = n log(n)`

You can easily spot if an algorithm has n log(n) time. Look for an outer loop that iterates through a list (n operations). Then look to see if there is an inner loop; If the inner loop is cutting down/reducing the data set on each iteration (log(n) operations), then the overall algorithm has a Big O (n log(n)).

Here’s a simple example of an algorithm with linearithmic time complexity:

```
function linearithmic(n) {
  for (let i = 0; i < n; i++) {
    for (let j = 1; j < n; j = j * 2) {
      console.log("Hello")
    }
  }
}
```

The outer loop iterates through 0 to n linearly (n) and the inner loop is log(n) because j is getting doubled on each loop.

Looking at it another way, if we double the size of our input, n, the outer loop will have twice as many iterations, whereas the inner loop would only have 1 extra iteration.

Linearithmic time is worse than linear time, O(n), but better than quadratic time, O(n^2).

A common, practical example of a linearithmic time complexity algorithm is the sorting algorithm Merge Sort - a divide and conquer style algorithm.

```
function mergeSort(arr) {
  // Base case
  if (arr.length <= 1) return arr;

  let mid = Math.floor(arr.length / 2);
  // Recursive calls
  let left = mergeSort(arr.slice(0, mid));
  let right = mergeSort(arr.slice(mid));

  return merge(left, right);
}

function merge(left, right) {
  let sortedArr = []; // the sorted items will go here

  while (left.length && right.length) {
    // Insert the smallest item into sortedArr
    if (left[0] < right[0]) {
      sortedArr.push(left.shift());
    } else {
      sortedArr.push(right.shift());
    }
  }

  // Use spread operators to create a new array, combining the three arrays
  return [...sortedArr, ...left, ...right];
}

console.log(mergeSort([3, 5, 8, 5, 99, 1])); // [1, 3, 5, 5, 8, 99]
```

### Space Complexity of Merge Sort

Merge Sort is very fast for a sorting algorithm, but as with most algorithms, the gains in speed come with the cost of taking up more space in memory. The larger the array, the more arrays that have to be stored in memory.
The space complexity of Merge Sort is O(n).

Performance summary table

![alt text](https://www.doabledanny.com/static/07bb2f1355bef36bef1c768a471a6e84/93d59/7.jpg)

## Big O(2^n) Exponential time complexity

An algorithm with exponential time complexity is one where the number of operations doubles every time we increase the input by one.

![alt text](https://www.doabledanny.com/static/445d073812759c19aa9b83d6ff239355/93d59/4.jpg)

Exponential time is the opposite of logarithmic time. With log time, every time we double the input, the number of operations increases by just 1.

An example of an `O(2^n)` function is the recursive calculation of Fibonacci numbers.

```
function fibonacci(num) {
  // Base cases
  if (num <= 1) return num;

  // Recursive part
  return fibonacci(num - 1) + fibonacci(num - 2);
}

fibonacci(1);
```

## Big O(n!) Factorial time complexity

Factorial time is when the runtime scales factorially as the input grows. For an example, the factorial of 5 would be the product of `5*4*3*2*1`. An example of an algorithm that would have a factorial run time, would calculate every combination of a set.

Example:

```
function getPermutations(string, prefix = "") {
  if (string.length <= 1) {
    return [prefix + string];
  }

  return Array.from(string).reduce((result, char, index) => {
    const reminder = string.slice(0, index) + string.slice(index + 1);
    result = result.concat(getPermutations(reminder, prefix + char));

    return result;
  }, []);
}

console.log(getPermutations("abc")); // ['abc', 'acb', 'bac', 'bca', 'cab', 'cba']
```
