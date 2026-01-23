# Bubble Sort

Imagine morning assembly in school.
All students must stand according to height — shortest in front, tallest at the back.
But today, they’re standing randomly.

What the teacher does (Bubble Sort):

- The teacher looks at two students standing next to each other.
- If the taller student is in front of the shorter one,
👉 the teacher tells them to swap places.
- The teacher moves to the next pair and does the same check.
- This continues till the last student.

After one round:

- The tallest student reaches the back of the line.

- Then the teacher starts again from the front of the line.

- They repeat this until:

- Everyone is standing properly height-wise,

- No swapping is needed.

---

```cpp
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

```
