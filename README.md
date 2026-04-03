# 🔎 Mini Search Engine (C++)

A simple mini search engine built using C++.  
It searches for a keyword across multiple text files and shows results based on frequency.

---

## ✦ Features

➤ Search keyword across multiple files  
➤ Case-insensitive search (Java = java)  
➤ Counts number of matches  
➤ Clean and readable output  

---

## ✦ What I learned

➤ File handling in C++  
➤ String searching and manipulation  
➤ Writing structured and readable code  
➤ Basic idea of how search systems work  

---

## ✦ Project Structure
```
mini-search-engine/
│── main.cpp
│── data/
│   ├── file1.txt
│   ├── file2.txt
│   └── file3.txt
│── output.png
│── README.md
```                                                                                                                                                                                                                                                                                                ## Code

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

// convert text to lowercase
string toLower(string text) {
    for (char &c : text) {
        c = tolower(c);
    }
    return text;
}

// function to count matches in a file
int countMatches(string filename, string keyword) {
    ifstream file(filename);
    string line;
    int count = 0;

    while (getline(file, line)) {
        if (toLower(line).find(toLower(keyword)) != string::npos) {
            count++;
        }
    }

    return count;
}

int main() {
    string keyword;
    cout << "Enter keyword: ";
    cin >> keyword;

    vector<pair<string, int>> results;

    // check all files
    results.push_back({"file1.txt", countMatches("data/file1.txt", keyword)});
    results.push_back({"file2.txt", countMatches("data/file2.txt", keyword)});
    results.push_back({"file3.txt", countMatches("data/file3.txt", keyword)});

    // sort by highest matches
    sort(results.begin(), results.end(), [](auto &a, auto &b) {
        return a.second > b.second;
    });

    cout << "\nSearch Results:\n";

    for (auto r : results) {
        if (r.second > 0) {
            cout << r.first << " contains " << r.second << " matches" << endl;
        }
    }

    return 0;
}
```
