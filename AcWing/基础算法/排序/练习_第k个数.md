```
#include <iostream>
using namespace std;

void qort_sort(int nums[], int low, int high){
    int l = low, r = high;
    if (l < r){
        swap(nums[l], nums[(l+r)/2]);
        int pivot = nums[l];
        while (l < r){
            while (l < r && nums[r] > pivot) r--;
            if (l < r) nums[l++] = nums[r];
            while (l < r && nums[l] < pivot) l++;
            if (l < r) nums[r--] = nums[l];
        }
        nums[l] = pivot;
        qort_sort(nums, low, l-1);
        qort_sort(nums, l+1, high);
    }

}

int main(){
    int n, k;
    scanf("%d %d", &n, &k);
    int nums[100005];
    for (int i = 0; i < n; i++){
        scanf("%d", &nums[i]);
    }
    qort_sort(nums, 0, n-1);
    printf("%d\n", nums[k-1]);

    return 0;
}

```
