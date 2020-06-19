# Nuts and bolts problem.

Problem statement: Given a set of n nuts of different sizes and n bolts of different sizes. There is a one-one mapping between nuts and bolts. Match nuts and bolts efficiently.

```
// O(N) time complexity, O(N) space complexity

#include<bits/stdc++.h>

using namespace std;

unordered_map<int, int> matchNutsAndBolts(vector<int>& nuts, vector<int>& bolts) {
    unordered_map<int, int> dict;
    for (int i = 0; i < nuts.size(); i++) {
        dict[nuts[i]] = i;
    }

    for (int i = 0; i < bolts.size(); i++) {
        int temp = dict[bolts[i]];
        dict.erase(bolts[i]);
        dict.emplace(temp, i);
    }

    return dict;
}

int main() {
    srand(time(NULL));

    vector<int> nuts;
    for (int i = 0; i < 10; i++) {
        nuts.push_back(i);
    }

    vector<int> bolts(nuts);

    for (int i = 1; i < bolts.size(); i++) {
        int randIndex = rand()%i;
        swap(bolts[i], bolts[randIndex]);
    }

    unordered_map<int, int> nutsBoltsMap = matchNutsAndBolts(nuts, bolts);

    for (auto it = nutsBoltsMap.begin(); it != nutsBoltsMap.end(); ++it) {
        assert(nuts[it->first] == bolts[it->second]);
    }

    return 0;
}
```
