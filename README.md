Parlindromic
============
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:yanfanyu/Parlindromic.git
git push -u origin master
// Type your C++ code and click the "Run Code" button!
// Your code output will be shown on the left.
// Click on the "Show input" button to enter input data to be read (from stdin).

#include <iostream>
#include <string>
#include <queue>

using namespace std;

#define max 1000

int path[max];

void dfs(string s, int start, int n, bool table[max][max], int m){

    if(start==n){
        cout << "  [";
        int j = 0;
        for(int i=0; i<m-1; ++i){
            cout << "\"" << s.substr(j, path[i]-j+1) << "\",";
            j = path[i]+1;
        }
        cout << "\"" << s.substr(j, path[m-1]-j+1) << "\"" << "]" << endl;
        return;
    }
    
    for(int i=start; i<n; ++i){
        if(table[start][i]){
            path[m] = i;
            dfs(s, i+1, n, table, m+1);
        }
    }
}

void PalindromeDP(string s){
    int n = s.length();
    bool table[max][max] = {false};

    for(int i=0; i<n; ++i)
        table[i][i] = true;
    for(int i=0; i<n-1; ++i)
        if(s[i]==s[i+1])
            table[i][i+1] = true;

    for(int len=3; len<=n; ++len)
        for(int i=0; i<n-len+1; ++i){
            int j=i+len-1;
            if(s[i]==s[j] && table[i+1][j-1])
                table[i][j] = true;
        }
    if(n == 0){
        cout << "[" << endl << "]";
        return;
    }

    int m = 0;    

    cout << "[" << endl;
    dfs(s, 0, n, table, m);
    cout << "]";
}


int main() {

    string s;
    cin >> s;
    PalindromeDP(s);

    return 0;
}
