---
layout: post
title: C++ Practice with Divide and Conquer Algorithms
excerpt: "Merge sort and inversion count"
categories: [C++, algorithms]
comments: true
---

Recently I've been working on an [algorithms course](https://lagunita.stanford.edu/courses/course-v1:Engineering+Algorithms1+SelfPaced/info) hosted at Stanford University. The concept of divide and conquer was introduced through merge sort, which I wanted to be able to code in C++. My first attempts tried to follow merge sort pseudocode which I found online, but this didn't work because I found out that C++ doesn't allow variable length arrays! Being a complete programming amateur, I decided that it would probably be better to try and analyse the code of other's online, since I didn't fully understand recursive functions either. I came across [Hong's many implementations of merge sort](http://www.bogotobogo.com/Algorithms/mergesort.php) and decided to follow the one which used the actual input array itself. 

I feel like the trickiest part about this algorithm is understanding how the recursive 'mergeSort' function works. One of the analogies which really helped my understanding was actually related to Inception (yes, the movie about dreams!). The levels of the recursive function can be thought of as nested dreams, and lower dream (level) must be completed before moving to a higher dream. The function ends when the topmost level is completed. Another really helpful method was using the 'step in' and 'step over' debug options in Visual Studio to see which order the lines of code were being executed. 

In the end, I tried coding the merge sort from scratch, and this is what I ended up with:

~~~ c
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
			tempPos++;p
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
~~~

When comparing it with Hong's code, it is obviously inspired and mainly similar. The main difference which I could spot was this line:

~~~ c 
if ((a[left] < a[right] && left <= mid) || right > high)
~~~

I condensed the extreme cases (e.g. [1,2,3,4,5,6] and [6,5,4,3,2,1]) into conditions which were included in the if statement. It seems to exploit the fact that C++ doesn't return "array out of bounds exception" error. I'm not sure whether this is a good solution but I've yet to find test cases where this doesn't work! 

This merge sort implementation could be easily modified to count the number of inversions. By adding a global variable ~~~ invCount ~~~ 
