Parlindromic
============

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

class Solution {
public:

    void dfs(string s, int start, int n, bool table[1000][1000], int m, int min){

        if(start==n){
            if(m < min) min = m;
        }
        
        for(int i=start; i<n; ++i){
            if(table[start][i]){
                dfs(s, i+1, n, table, m+1);
            }
        }
    }
    
    int minCut(string s) {
        
        int n = s.length();
        bool table[1000][1000] = {false};
    
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
        if(n == 0)
            return 0;
    
        int m = 0, min = 0;    
        dfs(s, 0, n, table, m, min);
        return min;
    }

};
