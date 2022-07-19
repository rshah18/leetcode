```cpp

int balancedSum(vector<int> arr) {
  unordered_map<int, int> rmap; 
  unordered_map<int, int> lmap; 

  int rindex = arr.size()-1; 
  int lindex = 0; 
  int sumr = 0; 
  int suml = 0; 
  while(lindex < arr.size()){
    // left sum 
    suml += arr[lindex]; 
    lmap[lindex] = suml; 
    lindex++; 

    // right sum
    sumr += arr[rindex]; 
    rmap[rindex] = sumr; 
    rindex--; 
  }

  for(int i = 1; i < arr.size(); i++){
    if(lmap[i-1] == rmap[i+1]){
      return i; 
    }
  }

  return 0;


}



long maxPoints(vector<int> elements) {
    long sum = 0; 
    if(elements.size() <= 10000){
           
        map<int, int> memo; 


        for(auto a: elements){
            memo[a]++;     
        }

        int skipItem = 0; 
        for(auto it = memo.rbegin(); it != memo.rend(); it++){
            cout << it->first <<" " << it->second << endl; 
            

            if(skipItem != it->first){
                sum += it->first * it->second; 
                skipItem = it->first-1; 
                cout << "added " << it->first << endl; 
            }
            
        }
        cout << sum << endl; 
    }
  return sum; 

}
```

