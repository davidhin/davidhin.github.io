---
layout: post
title: C++ Practice with Divide and Conquer Algorithms
excerpt: "Featuring: merge sort, inversion counts and more"
categories: [C++, algorithms]
comments: true
---

Recently I've been working on an [algorithms course](https://lagunita.stanford.edu/courses/course-v1:Engineering+Algorithms1+SelfPaced/info) hosted at Stanford University. The concept of divide and conquer was introduced through merge sort, which I wanted to be able to code in C++. 

~~~ cpp
int main() {
	int arr[] = { 1,5,2,3,4 };
	int arrSize = sizeof(arr) / sizeof(int);

	mergeSort(arr, 0, arrSize - 1);
	printArr(arr, arrSize);

	return 0;
}
~~~
