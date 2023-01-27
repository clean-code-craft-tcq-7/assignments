# TDD First step - recap

[Data-driven tests](https://github.com/clean-code-craft-tcq-7/tdd-buckets-omprakashs855/blob/f63148ecf5b817958e2b956a79b2234b9a4c9edf/inc/test_case.json)

---

Call a function by its purpose, not by its code

```c
int cmpfunc (const void * a, const void * b) {
   return ( *(int*)a - *(int*)b );
}

qsort(reading, size, sizeof(int), cmpfunc);
```

The code of `cmpfunc` is to compare. Its purpose is to sort in ascending order.
Try a name like `compareForAscending`

---

This function scans the numbers till it finds something with a "difference of two or more".
Calling it `scanConsecutiveNumbers` would simplify it to one `for` and one `if`?

```python
def multiple_data_check(self, data, nested_list, max_idx):
  max_idx = 0
  for idx, val in enumerate(data):
    if (val - data[max_idx]) == 0:
      nested_list.append(val)
    elif (val - data[max_idx]) == 1:
      max_idx = idx
      nested_list.append(val)
    else:
      break
  return nested_list, idx
```

---

Use test names / strings to express functionality. Also, `assertTrue` is stronger at expressing, than `assertFalse`.

```java
@Test
public void checkRangesMoreDataFailed() {
    ArrayList<Integer> inputData = new ArrayList<>(Arrays.asList(1, 9, 6, 7, 8, 9, 10, 11));
    Map<String, Integer> result = chargingRange.calculateRanges(inputData);
    assertFalse(result.get("7 - 10") == null);
    assertFalse(result.get("1 - 1") == 2);
}
```
