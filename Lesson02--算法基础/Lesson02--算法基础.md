# 2. 算法基础

## 2.1 插入排序

**输入:** $<a_1,a_2,...,a_n>$
**输出:** $<a_1^{'},a_2^{'},...,a_n^{'}>,(a_1^{'} \leqslant a_2^{'} \leqslant ... \leqslant a_n^{'})$

```C++{.line-numbers}
#include<iostream>
#include<vector>
using namespace std;
void INSERTION_SORT(vector<int>& v)
{
	for (int j = 1; j < v.size(); j++)
	{
		int key = v[j];
		int i = j - 1;
		while (i >= 0 && v[i] > key)
		{
			v[i + 1] = v[i];
			--i;
		}
		v[i + 1] = key;
	}
}
int main()
{
	vector<int> v = { 5,2,4,6,1,3,9,10,7,8 };
	INSERTION_SORT(v);
	for (auto e : v)
		cout << e << " ";
	return 0;
}
```

* **循环不变式与插入排序的正确性**
  我们常常使用 **循环不变式(Loop Invariant)** 来证明增量法的正确性.
  关于循环不变式,我们必须证明三条性质:
  * **初始化(Initialization)** :循环的第一次迭代之前,它为真.
  * **保持(Maintenance)** :如果循环的某次迭代之前它为真,那么下次迭代之前它仍为真.
  * **终止(Termination)** :在循环终止时,不变式为我们提供一个有用的性质,该性质有助于证明算法是正确的.
  
  本质: **数学归纳法(Mathematics Induction)** .

## 2.2 分析算法

* 随机访问机模型
  * 我们假定一种通用的单处理器计算模型: **随机访问机(Random Access Machine,RAM)** .
  * 在RAM模型中,指令一条接一条地执行,没有并发操作.
  * 支持常数项时间的算术指令,数据移动指令和控制指令.

* 运行时间
  * 通常把一个算法的运行时间描述成其输入规模的函数.
  * 输入规模的粒度是视具体问题而定的.
    * 排序问题:排序元素的个数.
    * 整数乘法问题:乘数的位数.
    * 图问题:图上的结点数和边数.
  * 给定输入后,运行时间就是该输入下基本操作的次数.

* 最坏情况与平均情况分析
  * 通常,我们只关心最坏情况下算法的运行时间.
    * 最坏情况下的运行时间给出了任何输入下运行时间的一个上界.
    * 对某些算法,最坏情况经常出现.
    * 平均情况往往和最坏情况一样.
  * 平均情况.

* 增长量级
  * 更简化的抽象-- **增长量级/增长率(Order-of-Growth)** .
    * 忽略低阶项.
    * 忽略高阶项系数.
  * 当n足够大时,低阶项和系数相对来说不如增长率重要.

## 2.3 设计算法

### 2.3.1 分治法

许多有用的算法在结构上时递归的,为了解决一个给定的问题,算法一次或多次递归地调用其自身以解决紧密相关的若干子问题.这些算法典型地遵循 **分治法(Divide and Conquer)** 的思想:将原问题分解为几个规模较小但类似于原问题的子问题,递归地求解这些子问题,然后再合并这些子问题的解来建立原问题的解.

* **分(Divide)** :分解原问题为子问题,子问题是原问题规模较小的实例.
* **治(Conquer)** :解决子问题--递归地解决或者直接求解.
* **合(Combine)** :将子问题的解合并成原问题的解.

**归并排序**

```C++{.line-numbers}
#include<iostream>
#include<vector>
using namespace std;
template <class T>
void MERGE(vector<T>& v, size_t left, size_t mid, size_t right)
{
    size_t n1 = mid - left + 1;
    size_t n2 = right - mid;
    vector<T> L(n1);
    vector<T> R(n2);
    for (size_t i = 0; i < n1; ++i)
        L[i] = v[left + i];
    for (size_t j = 0; j < n2; ++j)
        R[j] = v[mid + 1 + j];
    size_t i = 0;
    size_t j = 0;
    size_t k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            v[k] = L[i];
            ++i;
        }
        else {
            v[k] = R[j];
            ++j;
        }
        ++k;
    }
    while (i < n1) {
        v[k] = L[i];
        ++i;
        ++k;
    }
    while (j < n2) {
        v[k] = R[j];
        ++j;
        ++k;
    }
}
template<class T>
void MERGE_SORT(vector<T>& v, size_t left, size_t right)
{
	if (left < right)
	{
		int mid = (left + right) / 2;
		MERGE_SORT(v, left, mid);
		MERGE_SORT(v, mid + 1, right);
		MERGE(v, left, mid, right);
	}
}
int main()
{
	vector<int> v = { 5,4,6,3,9,8,10,2,1,7 };
	MERGE_SORT(v, 0, v.size()-1);
	for (auto e : v)
		cout << e << " ";
	return 0;
}
```

### 2.3.2 分析分治算法