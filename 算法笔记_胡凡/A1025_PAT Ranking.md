```c++
#include <cstdio>
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

class Testee{
public:
    string idNumber;
    int score;
    int localRank;
    int locationNumber;
    Testee(string _idNumber, int _score, int _locationNumber)
        :idNumber(_idNumber), score(_score), locationNumber(_locationNumber) { }
};

bool cmp(const Testee &lhs, const Testee &rhs){
    if (lhs.score > rhs.score || (lhs.score == rhs.score && lhs.idNumber < rhs.idNumber))
        return true;
    else
        return false;
}

int main() {
    int n;
    scanf("%d", &n);
    vector<Testee> rec;
    int count = 0;
    for (int i = 0; i < n; ++i) {
        int m;
        scanf("%d", &m);
        count += m;
        vector<Testee> temp;
        for (int j = 0; j < m; ++j) {
            string str;
            char strArray[20];
            int score;
            scanf("%s %d", strArray, &score);
            str = strArray;
            temp.push_back(Testee(str,score,i+1));
        }
        sort(temp.begin(),temp.end(),&cmp);

        for (int j = 0; j < temp.size(); ++j) {
            if (j == 0)
                temp[j].localRank = j+1;
            else{
                if (temp[j].score == temp[j-1].score){
                    temp[j].localRank = temp[j-1].localRank;
                }else{
                    temp[j].localRank = j+1;
                }
            }

            rec.push_back(temp[j]);
        }

    }
    sort(rec.begin(), rec.end(), &cmp);

    printf("%d\n", count);
    int rank;
    for (int i = 0; i < rec.size(); ++i) {
        if (i == 0){
            rank = i+1;
        }else{
            if (rec[i].score != rec[i-1].score){
                rank = i+1;
            }
        }
        printf("%s %d %d %d\n",rec[i].idNumber.c_str(),rank,rec[i].locationNumber,rec[i].localRank);
    }

    return 0;
}
```
