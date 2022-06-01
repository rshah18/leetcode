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