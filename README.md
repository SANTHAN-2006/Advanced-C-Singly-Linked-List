# Advanced-C-Singly-Linked-List


### Objective:
- Implement a list using an array to store elements.
- Perform operations like:
  1. Inserting an element at the beginning, middle, or end of the list.
  2. Deleting an element from the beginning, middle, or end.
  3. Searching for an element in the list.
  4. Displaying the list contents.

---

### 1. **Setting Up the Array and Size**

```c
#define MAX 100 
int list[MAX];  
int size = 0;   
```

- `MAX` defines the maximum capacity of our list (100 elements in this case).
- `list[]` is the array that will hold the elements of the list.
- `size` is a variable that keeps track of how many elements are currently in the list.

---

### 2. **Insertion Functions**

#### **a) Insert at the Beginning**

```c
void insertAtBeginning(int value) {
    if (size >= MAX) {
        printf("List is full\n");
        return;
    }
    for (int i = size; i > 0; i--) {
        list[i] = list[i - 1];
    }
    list[0] = value;
    size++;
}
```

- **Explanation**:
  - If the list is full (`size >= MAX`), we cannot insert, so we print "List is full."
  - We shift all elements to the right by 1 position (`for (int i = size; i > 0; i--)`).
  - Insert the new value at position `0`.
  - Increment `size` to reflect the new element.

#### **b) Insert at the End**

```c
void insertAtEnd(int value) {
    if (size >= MAX) {
        printf("List is full\n");
        return;
    }
    list[size] = value;
    size++;
}
```

- **Explanation**:
  - If the list is full, print "List is full."
  - Insert the new element at the current end (`list[size]`).
  - Increment `size` to account for the new element.

#### **c) Insert at the Middle (Specified Position)**

```c
void insertAtMiddle(int value, int position) {
    if (size >= MAX) {
        printf("List is full\n");
        return;
    }
    if (position < 1 || position > size + 1) {
        printf("Invalid position\n");
        return;
    }
    for (int i = size; i >= position; i--) {
        list[i] = list[i - 1];
    }
    list[position - 1] = value;
    size++;
}
```

- **Explanation**:
  - If the list is full, print "List is full."
  - If the position is invalid (less than 1 or greater than `size + 1`), print "Invalid position."
  - Shift all elements starting from the position to the right to make room for the new element.
  - Insert the new element at the specified position.
  - Increment `size`.

---

### 3. **Deletion Functions**

#### **a) Delete from the Beginning**

```c
void deleteAtBeginning() {
    if (size == 0) {
        printf("List is empty\n");
        return;
    }
    for (int i = 0; i < size - 1; i++) {
        list[i] = list[i + 1];
    }
    size--;
}
```

- **Explanation**:
  - If the list is empty, print "List is empty."
  - Shift all elements to the left to fill the gap left by the deleted element.
  - Decrement `size` to reflect the removal.

#### **b) Delete from the End**

```c
void deleteAtEnd() {
    if (size == 0) {
        printf("List is empty\n");
        return;
    }
    size--;
}
```

- **Explanation**:
  - If the list is empty, print "List is empty."
  - Just decrement `size` to remove the last element, as no shifting is needed.

#### **c) Delete from the Middle (Specified Position)**

```c
void deleteAtMiddle(int position) {
    if (size == 0) {
        printf("List is empty\n");
        return;
    }
    if (position < 1 || position > size) {
        printf("Invalid position\n");
        return;
    }
    for (int i = position - 1; i < size - 1; i++) {
        list[i] = list[i + 1];
    }
    size--;
}
```

- **Explanation**:
  - If the list is empty, print "List is empty."
  - If the position is invalid, print "Invalid position."
  - Shift elements from the specified position to the left to fill the gap left by the deleted element.
  - Decrement `size`.

---

### 4. **Search for an Element**

```c
void search(int value) {
    for (int i = 0; i < size; i++) {
        if (list[i] == value) {
            printf("Element %d found at position %d\n", value, i + 1);
            return;
        }
    }
    printf("Element %d not found in the list\n", value);
}
```

- **Explanation**:
  - Iterate through the list (`for (int i = 0; i < size; i++)`) and check if the current element is equal to `value`.
  - If found, print its position (`i + 1`).
  - If not found, print that the element was not found.

---

### 5. **Display the List**

```c
void display() {
    if (size == 0) {
        printf("List is empty\n");
        return;
    }
    printf("List elements: ");
    for (int i = 0; i < size; i++) {
        printf("%d ", list[i]);
    }
    printf("\n");
}
```

- **Explanation**:
  - If the list is empty, print "List is empty."
  - Otherwise, iterate through the array and print each element.

---

### 6. **Main Function**

```c
int main() {
    int choice, value, pos;

    do {
        printf("\n1. Insert at Beginning\n2. Insert at End\n3. Insert at Middle\n4. Delete at Beginning\n5. Delete at End\n6. Delete at Middle\n7. Search\n8. Display\n9. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter value to insert at beginning: ");
                scanf("%d", &value);
                insertAtBeginning(value);
                break;
            case 2:
                printf("Enter value to insert at end: ");
                scanf("%d", &value);
                insertAtEnd(value);
                break;
            case 3:
                printf("Enter value to insert at middle: ");
                scanf("%d", &value);
                printf("Enter position: ");
                scanf("%d", &pos);
                insertAtMiddle(value, pos);
                break;
            case 4:
                deleteAtBeginning();
                break;
            case 5:
                deleteAtEnd();
                break;
            case 6:
                printf("Enter position to delete: ");
                scanf("%d", &pos);
                deleteAtMiddle(pos);
                break;
            case 7:
                printf("Enter value to search: ");
                scanf("%d", &value);
                search(value);
                break;
            case 8:
                display();
                break;
            case 9:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice, please try again.\n");
        }
    } while (choice != 9);

    return 0;
}
```

- **Explanation**:
  - Continuously prompt the user to select an operation.
  - Based on the user's choice, call the respective function (insertion, deletion, search, or display).
  - The program exits when the user chooses option 9 (`Exit`).

---

### Final Output:
![image](https://github.com/user-attachments/assets/e716a0e0-0856-44ae-ac1e-b1f77b7a664f)
