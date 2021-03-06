# c++ basic algorithms

## Sorting

#### Bubble sort

```cpp
void bubbleSort(vector<int>& v){
  bool isSorted = false;
  int lengthLeft = v.size()-1;
  while(!isSorted){
    isSorted = true;
    for(int i = 0; i < lengthLeft; i++ ){
      if(v[i] > v[i+1]){
        swap(v[i], v[i+1]);
        isSorted = false;
      }
    }
    lengthLeft--;
  }
}
```

#### insertion sort

```cpp
void insertionSort(vector<int> & v){
  for(int i = 1; i < v.size(); i++){
    for(int j = i; j > 0; j--){
      if(v[j] < v[j-1]){
        swap(v[j], v[j-1]);
      }
    }
  }
}

void betterInsertionSort(vector<int> &v){
  for(int i = 1; i < v.size(); i++){
    int j = i;
    int current = v[j];
    while(j > 0 && current < v[j-1]){
      v[j] = v[j-1];
      j--;
    }
    v[j] = current;
  }

}
```

#### selection sort

```cpp
void selectionSort(vector<int> &v){
  cout << "Selection sort: " << endl;

  for(int i = 0; i < v.size(); i++){
    int smallestValueIndex = i;
    for(int j = i; j < v.size(); j++){
      if(v[j] < v[smallestValueIndex] ){
        swap(smallestValueIndex, j);
      }
    }

    swap(v[smallestValueIndex], v[i]);
  }
}
```

* Selection sort begins at index 0. 
* first pass searches for smallest item in the whole list and  puts it at index 0
* and then second pass searches through from index 1 to end-1 and puts it at index 1
* so on. 



#### quick sort

* Pivot
  * Correct position in final, sorted array
  * Items to the left are smaller
  * Items to the right are larger
* choosing pivot
  * we want to pick a pivot that divides in half or close to it. 

```cpp
int partition(vector<int> &v, int left, int right, int pivotIndex){
  while(left <= right){
    while(v[left] < v[pivotIndex]){
      left++;
    }

    while(v[right] > v[pivotIndex]){
      right--;
    }

    if(left <= right){
      swap(v[left], v[right]);
      left++;
      right--;
    }

  }
  return left;
}

void quickSort(vector<int> &v, int left, int right){

    if(left >= right){
      return;
    }

    // pick a pivot index 
    int pivotIndex = (left+right)/2;

    // partition the array around the pivot
    int index = partition(v, left, right, pivotIndex);
    
    quickSort(v, left, index-1);
    quickSort(v, index, right);

}
```

#### merge sort

* 