# merge-and-selection-sort
merge and selection sort
# Employee Records Sorting using Selection Sort and Merge Sort in C

## 📌 Overview

This program demonstrates sorting employee records based on the **average of height and weight**.  
It uses **Selection Sort** and **Merge Sort** algorithms and dynamically allocates memory for employee records.  

Each employee has the following details:  
- Name  
- Height  
- Weight  
- Average of Height and Weight  

---

## 📌 Algorithm

**Selection Sort Algorithm**  
1. Traverse the array to find the minimum average value.  
2. Swap it with the first unsorted element.  
3. Repeat for all elements until sorted.  

**Merge Sort Algorithm**  
1. Divide the array into two halves.  
2. Recursively sort the left and right halves.  
3. Merge the two sorted halves to form the final sorted array.  

---

## 📌 Pseudocode
```
START

Input number of employees: n

Allocate memory for n employees

FOR i = 0 to n-1
Input Name, Height, Weight
Calculate Average = (Height + Weight)/2
END FOR

PRINT all employee details

// SELECTION SORT
FOR i = 0 to n-1
Find employee with minimum average in remaining array
Swap with current employee
END FOR
PRINT sorted employee details

// MERGE SORT
FUNCTION mergeSort(start, end)
IF start < end
mid = (start + end)/2
mergeSort(start, mid-1)
mergeSort(mid+1, end)
merge(start, mid, end)
END IF
END FUNCTION
PRINT sorted employee details

Free allocated memory

END
```


---

## 📌 Dry Run Example

### Input:
```
Number of employees: 3
Employee Details:
Name: Abir, Height: 160, Weight: 70
Name: Aarav, Height: 150, Weight: 80
Name: Isha, Height: 170, Weight: 60
```


### Step 1: Calculate Average
```
Abir → (160+70)/2 = 115
Aarav → (150+80)/2 = 115
Isha → (170+60)/2 = 115
```

### Step 2: Selection Sort
- Array is already sorted based on average → No swaps required.  

### Step 3: Merge Sort
- Divide array into halves  
- Merge sorted halves → Array remains the same  

### Output:
```
Name: Abir || Height: 160 || Weight: 70 || Average: 115
Name: Aarav || Height: 150 || Weight: 80 || Average: 115
Name: Isha || Height: 170 || Weight: 60 || Average: 115
```

---
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <string>
using namespace std;

struct employee_Vnk {
    string name_Vnk;
    int height_Vnk;
    int weight_Vnk;
    int average_Vnk;
};

void selectionSort_Vnk(employee_Vnk* emp_Vnk, int n_Vnk);
void mergeSort_Vnk(employee_Vnk* emp_Vnk, int start_Vnk, int end_Vnk);
void merge_Vnk(employee_Vnk* emp_Vnk, int start_Vnk, int mid_Vnk, int end_Vnk);

int main() {
    srand(time(0));

    int n_Vnk;
    cout << "Enter the number of employee details you want: ";
    cin >> n_Vnk;

    string names_Vnk[] = { "Abir","Aarav","Isha","Rohan","Priya","Vikas","Neha","Sahil","Anaya","Dev","Kriti",
        "Mira","Kabir","Tanvi","Yash","Riya","Arjun","Asha","Nikhil","Pooja","Kunal",
        "Vishal","Amir","Sharukh","Salman","Mrunal","Kirti" };
    int name_size_Vnk = sizeof(names_Vnk) / sizeof(names_Vnk[0]);

    employee_Vnk* emp_Vnk = new employee_Vnk[n_Vnk];

    for (int i_Vnk = 0; i_Vnk < n_Vnk; i_Vnk++) {
        emp_Vnk[i_Vnk].name_Vnk = names_Vnk[rand() % name_size_Vnk];
        emp_Vnk[i_Vnk].height_Vnk = rand() % (180 - 150 + 1) + 150;
        emp_Vnk[i_Vnk].weight_Vnk = rand() % (100 - 60 + 1) + 60;
        emp_Vnk[i_Vnk].average_Vnk = (emp_Vnk[i_Vnk].height_Vnk + emp_Vnk[i_Vnk].weight_Vnk) / 2;
    }

    cout << "\nOriginal Employee Records:\n";
    for (int i_Vnk = 0; i_Vnk < n_Vnk; i_Vnk++) {
        cout << "Name: " << emp_Vnk[i_Vnk].name_Vnk
             << " || Height: " << emp_Vnk[i_Vnk].height_Vnk
             << " || Weight: " << emp_Vnk[i_Vnk].weight_Vnk
             << " || Average: " << emp_Vnk[i_Vnk].average_Vnk << "\n";
    }

    cout << "\n------- SELECTION SORT ----------\n";
    selectionSort_Vnk(emp_Vnk, n_Vnk);

    cout << "\n--------- MERGE SORT -----------\n";
    mergeSort_Vnk(emp_Vnk, 0, n_Vnk - 1);
    for (int i_Vnk = 0; i_Vnk < n_Vnk; i_Vnk++) {
        cout << "Name: " << emp_Vnk[i_Vnk].name_Vnk
             << " || Height: " << emp_Vnk[i_Vnk].height_Vnk
             << " || Weight: " << emp_Vnk[i_Vnk].weight_Vnk
             << " || Average: " << emp_Vnk[i_Vnk].average_Vnk << "\n";
    }

    delete[] emp_Vnk;
    return 0;
}

void selectionSort_Vnk(employee_Vnk* emp_Vnk, int n_Vnk) {
    for (int i_Vnk = 0; i_Vnk < n_Vnk - 1; i_Vnk++) {
        int minIndex_Vnk = i_Vnk;
        for (int j_Vnk = i_Vnk + 1; j_Vnk < n_Vnk; j_Vnk++) {
            if (emp_Vnk[j_Vnk].average_Vnk < emp_Vnk[minIndex_Vnk].average_Vnk) {
                minIndex_Vnk = j_Vnk;
            }
        }
        swap(emp_Vnk[i_Vnk], emp_Vnk[minIndex_Vnk]);
    }

    for (int i_Vnk = 0; i_Vnk < n_Vnk; i_Vnk++) {
        cout << "Name: " << emp_Vnk[i_Vnk].name_Vnk
             << " || Height: " << emp_Vnk[i_Vnk].height_Vnk
             << " || Weight: " << emp_Vnk[i_Vnk].weight_Vnk
             << " || Average: " << emp_Vnk[i_Vnk].average_Vnk << "\n";
    }
}

void mergeSort_Vnk(employee_Vnk* emp_Vnk, int start_Vnk, int end_Vnk) {
    if (start_Vnk < end_Vnk) {
        int mid_Vnk = (start_Vnk + end_Vnk) / 2;
        mergeSort_Vnk(emp_Vnk, start_Vnk, mid_Vnk);
        mergeSort_Vnk(emp_Vnk, mid_Vnk + 1, end_Vnk);
        merge_Vnk(emp_Vnk, start_Vnk, mid_Vnk, end_Vnk);
    }
}

void merge_Vnk(employee_Vnk* emp_Vnk, int start_Vnk, int mid_Vnk, int end_Vnk) {
    int len1_Vnk = mid_Vnk - start_Vnk + 1;
    int len2_Vnk = end_Vnk - mid_Vnk;

    employee_Vnk* left_Vnk = new employee_Vnk[len1_Vnk];
    employee_Vnk* right_Vnk = new employee_Vnk[len2_Vnk];

    for (int i_Vnk = 0; i_Vnk < len1_Vnk; i_Vnk++) left_Vnk[i_Vnk] = emp_Vnk[start_Vnk + i_Vnk];
    for (int j_Vnk = 0; j_Vnk < len2_Vnk; j_Vnk++) right_Vnk[j_Vnk] = emp_Vnk[mid_Vnk + 1 + j_Vnk];

    int i_Vnk = 0, j_Vnk = 0, k_Vnk = start_Vnk;
    while (i_Vnk < len1_Vnk && j_Vnk < len2_Vnk) {
        if (left_Vnk[i_Vnk].average_Vnk <= right_Vnk[j_Vnk].average_Vnk) {
            emp_Vnk[k_Vnk++] = left_Vnk[i_Vnk++];
        } else {
            emp_Vnk[k_Vnk++] = right_Vnk[j_Vnk++];
        }
    }
    while (i_Vnk < len1_Vnk) emp_Vnk[k_Vnk++] = left_Vnk[i_Vnk++];
    while (j_Vnk < len2_Vnk) emp_Vnk[k_Vnk++] = right_Vnk[j_Vnk++];

    delete[] left_Vnk;
    delete[] right_Vnk;
}


##output

Enter the number of employee details you want: 3

Original Employee Records:
Name: Aarav || Height: 165 || Weight: 70 || Average: 117
Name: Isha  || Height: 172 || Weight: 65 || Average: 118
Name: Abir  || Height: 160 || Weight: 75 || Average: 117

------- SELECTION SORT ----------
Name: Aarav || Height: 165 || Weight: 70 || Average: 117
Name: Abir  || Height: 160 || Weight: 75 || Average: 117
Name: Isha  || Height: 172 || Weight: 65 || Average: 118

--------- MERGE SORT -----------
Name: Aarav || Height: 165 || Weight: 70 || Average: 117
Name: Abir  || Height: 160 || Weight: 75 || Average: 117
Name: Isha  || Height: 172 || Weight: 65 || Average: 118

![img alt](https://github.com/vijay1234nkanade-boop/merge-and-selection-sort/blob/main/WhatsApp%20Image%202025-09-22%20at%2019.02.19_6e041731.jpg?raw=true)

![img alt](https://github.com/vijay1234nkanade-boop/merge-and-selection-sort/blob/main/WhatsApp%20Image%202025-09-22%20at%2019.02.19_94727249.jpg?raw=true)
![img alt](https://github.com/vijay1234nkanade-boop/merge-and-selection-sort/blob/main/WhatsApp%20Image%202025-09-22%20at%2019.02.20_3404c907.jpg?raw=true)
