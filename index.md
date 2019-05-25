# First

[Markdown link test](_posts/2019-05-26-Graph.md)

## Hello World

~~~cpp
#include <stdio.h>

int main(void)
{
	printf("Hello World\n");
	return 0;
}
~~~

~~~cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void bubble_sort(int *arr, int size)
{
        int i, j, tmp;

        for (i = 0; i < size - 1; i++) {
                for (j = 0; j < size - 1 - i; j++) {
                        if (arr[j] > arr[j + 1]) {
                                tmp = arr[j];
                                arr[j] = arr[j + 1];
                                arr[j + 1] = tmp;
                        }
                }
        }
}

int main(void)
{
        int arr[] = { 9, 1, 8, 2, 7, 3, 6, 4, 5 };
        int i, size;

        size = sizeof(arr) / sizeof(arr[0]);

        for (i = 0; i < size; i++) {
                printf("%d  ", arr[i]);
        }
        printf("\n");

        bubble_sort(arr, size);

        for (i = 0; i < size; i++) {
                printf("%d  ", arr[i]);
        }
        printf("\n");

        return 0;
}
~~~
