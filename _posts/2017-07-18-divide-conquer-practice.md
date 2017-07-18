---
layout: post
title: C++ Practice with Divide and Conquer Algorithms
excerpt: "Featuring: merge sort, inversion counts and more"
categories: [C++, algorithms]
comments: true
---

Recently I've been working on an [algorithms course](https://lagunita.stanford.edu/courses/course-v1:Engineering+Algorithms1+SelfPaced/info) hosted at Stanford University. The concept of divide and conquer was introduced through merge sort, which I wanted to be able to code in C++. 

{% highlight css %} {% raw %}
void printArr(int arr[], int n, int start = 0) {
	std::cout << "[";
	for (int i = start; i < n; ++i) {
		std::cout << arr[i];
		if (i < n - 1) {
			std::cout << ", ";
		}
	}
	std::cout << "]" << std::endl;
}

void merge(int a[], int low, int mid, int high) {
	int arrSize = high - low + 1;

	int *temp = new int[arrSize];
	int left{ low };  // these will be used to iterate over the
	int right{ mid + 1 }; // left and right halves
	int tempPos{ 0 };

	while (left <= mid || right <= high) {
		if ((a[left] < a[right] && left <= mid) || right > high) {
			temp[tempPos] = a[left];
			left++;
			tempPos++;
		}
		else {
			temp[tempPos] = a[right];
			right++;
			tempPos++;
		}
	}

	// Put back into original array
	for (int i = 0; i <= high - low; ++i) {
		a[i + low] = temp[i];
	}
	delete[] temp;
}

void mergeSort(int a[], int low, int high) {
	if (low == high) return; 
	int mid = (low + high) / 2;
	mergeSort(a, low, mid); // left half of the array
	mergeSort(a, mid + 1, high); // right half of the array
	merge(a, low, mid, high);
}

int main() {
	int arr[] = { 1,5,2,3,4 };
	int arrSize = sizeof(arr) / sizeof(int);

	mergeSort(arr, 0, arrSize - 1);
	printArr(arr, arrSize);

	return 0;
}

{% endraw %}
