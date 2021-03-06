---
title: Switching from C to C++
layout: post
date: '2017-05-17'
---

Before we even begin, let's get our hands dirty. Say we are given to sort an array of strings. Here's what one could achieve with a program in C :

{% highlight c linenos %}
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int comparator (const void *a, const void *b) { 
    const char **ia = (const char **)a;
    const char **ib = (const char **)b;

    return strcmp (*ia, *ib);
} 

void print_sorted_stringarray (char **array, int len) { 
    int i;
    for(i = 0; i < len; ++i) 
        printf("%s | ", array[i]);

    putchar('\n');
} 

int main () {
    /*array to be sorted*/
    char *s[] = {"Alexia", "Celine", "Alex", "Billie", "Forest", "Bill"};

    /*sort the strings*/
    qsort (s, 6, sizeof (char *), comparator);

    /*print the sorted array*/
    print_sorted_stringarray (s, 6);

    return 0;
}
{% endhighlight %}

Creepy, isn't it?
In C++, this is as simple as :

{% highlight cpp linenos %}

#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

void print_sorted_stringarray (string s[], int len) { 
    for(int i = 0; i < len; ++i) 
        cout << s[i] << " | "; 
    
    cout << '\n';
} 

int main () {
    /*array to be sorted*/
    string s[] = {"Alexia", "Celine", "Alex", "Billie", "Forest", "Bill"};

    /*sort the strings*/
    sort (s, s + 6);

    /*print the sorted array*/
    print_sorted_stringarray (s, 6);

    return 0;
}

{% endhighlight %}


If you are unfamiliar with the library function **qsort()** you might want to peep into [this](http://www.geeksforgeeks.org/comparator-function-of-qsort-in-c/) or [this](https://www.tutorialspoint.com/c_standard_library/c_function_qsort.htm). It's not needed for now though. The C++ [sort()](http://www.cplusplus.com/reference/algorithm/sort/) function defined in the header **<<algorithm>>** is much easier to use in comparison.  
Also notice how the C++ [string](http://www.cplusplus.com/reference/string/string/) type replaces the more complicated **char*** or a **char[]** type that is normally used to represent a string in C.    

One no longer needs to specify the type when writing to the standard output as one did while using printf. Writing something like this would do:  
{% highlight cpp %}
  
	int a = 10, b = 20;
	cout << a << ' ' << b;
  
{% endhighlight %}  
Likewise, cin can be used to read values from the standard input in place of scanf.  
{% highlight cpp %}
  
	int a, b;
	cin >> a >> b;
  
{% endhighlight %}  
[Learn more about Basic I/O in C++....](http://www.cplusplus.com/doc/tutorial/basic_io/)  
    
Let's look at   
{% highlight cpp %}
  
	using namespace std;
  
{% endhighlight %}  
This tells the compiler that the namespace **std** is intended for use. Let's not dig into **namespaces** in a simple blog post. Only thing, without this line, one would need to replace **string** with **std::string**.  


Though one might be knowing that these two languages are syntactically similar to each other, one might come across something fancy from time to time (or ***code to code***). Take this snippet for instance:  
{% highlight cpp %}
  
  	int year;
  	cin >> year;
	/*check for a leap year*/
	if ((year % 4 == 0 and year % 100 != 0) or year % 400 == 0)
		cout << "Leap year!";
	else
		cout << "Not a leap year";
  
{% endhighlight %}   
Yes, one can actually use the pythonic **and**, **or** and **not** instead of the punctuations. 