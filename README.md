# 双指针
双指针在n数之和、归并排序、快速排序中的应用

# 快速排序

## 随机选择法

**fixedPositionPartition.cpp**

```cpp
#include <iostream>

//对区间[left, right]进行划分
int partition(int A[], int left, int right){
    int pivot = A[left];       //选择当前区间首元素作为pivot
    while(left < right){
        while(left < right && A[right] > pivot) right--; //反复左移right
        A[left] = A[right]; //将A[right]挪到A[left]处
        while(left < right && A[left] <= pivot) left++; //反复右移left
        A[right] = A[left]; //将A[left]挪到A[right]处
    }

    A[left] = pivot;    //把pivot放到left与right相遇的地方
    return left;        //返回相遇的地方
}

void quickSort(int A[], int left, int right){
    if(left < right){ //当前区间的长度超过1
        //根据当前序列的pivot 以pos下标为界将[left, right]一分为二
        int pos = partition(A, left, right);
        quickSort(A, left, pos - 1); //对左子区间递归进行快速排序
        quickSort(A, pos + 1, right); //对右子区间递归进行快速排序
    }
}

int main() {
    const int SIZE = 5;
    int arr[SIZE] = {5, 4, 2, 1, 3};


    // 输出交换后数组的内容
    std::cout << "快速排序前：" << std::endl;
    for (int i = 0; i < SIZE; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    quickSort(arr, 0, SIZE - 1);
    std::cout << "快速排序后：" << std::endl;
    for (int i = 0; i < SIZE; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```



## 三数取中法

**threeMedianPartition.cpp**

```cpp
#include <iostream>

void swap(int A[], int index1, int index2) {
    int temp = A[index1];
    A[index1] = A[index2];
    A[index2] = temp;
}

int find3MedianIndex(int A[], int first, int middle, int last) {
    return (A[first] > A[middle]) ?
           ((A[middle] > A[last]) ? middle : ((A[first] > A[last]) ? last : first)) :
           ((A[first] > A[last]) ? first : ((A[middle] > A[last]) ? last : middle));
}


//对区间[left, right]进行划分
int threeMedianPartition(int A[], int left, int right){
    //选择当前区间首中尾三个元素的中位数作为pivot
    int pivotIndex = find3MedianIndex(A, left, (left + right) / 2, right);
    swap(A, left, pivotIndex);    //将得到的中位数和首元素交换 => 固定位置法
    int pivot = A[left];
    while(left < right){
        while(left < right && A[right] > pivot) right--; //反复左移right
        A[left] = A[right]; //将A[right]挪到A[left]处
        while(left < right && A[left] <= pivot) left++; //反复右移left
        A[right] = A[left]; //将A[left]挪到A[right]处
    }

    A[left] = pivot;    //把pivot放到left与right相遇的地方
    return left;        //返回相遇的地方
}

void quickSort(int A[], int left, int right){
    if(left < right){ //当前区间的长度超过1
        //根据当前序列的pivot 以pos下标为界将[left, right]一分为二
        int pos = threeMedianPartition(A, left, right);
        quickSort(A, left, pos - 1); //对左子区间递归进行快速排序
        quickSort(A, pos + 1, right); //对右子区间递归进行快速排序
    }
}

int main() {
    const int SIZE = 5;
    int arr[SIZE] = {5, 4, 2, 1, 3};


    // 输出交换后数组的内容
    std::cout << "快速排序前：" << std::endl;
    for (int i = 0; i < SIZE; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    quickSort(arr, 0, SIZE - 1);
    std::cout << "快速排序后：" << std::endl;
    for (int i = 0; i < SIZE; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```



## 随机选择法

**randomPartition.cpp**

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>

void swap(int A[], int index1, int index2) {
    int temp = A[index1];
    A[index1] = A[index2];
    A[index2] = temp;
}


//对区间[left, right]进行划分
int randPartition(int A[], int left, int right){
    //生成[left,right]内的随机数
    int pivotIndex = (int)(1.0 * rand() / RAND_MAX * (right - left) + left);
    swap(A, left, pivotIndex);    //将得到的随机数和首元素交换 => 固定位置法
    int pivot = A[left];
    while(left < right){
        while(left < right && A[right] > pivot) right--; //反复左移right
        A[left] = A[right]; //将A[right]挪到A[left]处
        while(left < right && A[left] <= pivot) left++; //反复右移left
        A[right] = A[left]; //将A[left]挪到A[right]处
    }

    A[left] = pivot;    //把pivot放到left与right相遇的地方
    return left;        //返回相遇的地方
}

void quickSort(int A[], int left, int right){
    if(left < right){ //当前区间的长度超过1
        //根据当前序列的pivot 以pos下标为界将[left, right]一分为二
        int pos = randPartition(A, left, right);
        quickSort(A, left, pos - 1); //对左子区间递归进行快速排序
        quickSort(A, pos + 1, right); //对右子区间递归进行快速排序
    }
}

int main() {
    const int SIZE = 5;
    int arr[SIZE] = {5, 4, 2, 1, 3};


    // 输出交换后数组的内容
    std::cout << "快速排序前：" << std::endl;
    for (int i = 0; i < SIZE; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    quickSort(arr, 0, SIZE - 1);
    std::cout << "快速排序后：" << std::endl;
    for (int i = 0; i < SIZE; ++i) {
        std::cout << arr[i] << " ";
    }
    std::cout << std::endl;

    return 0;
}
```


