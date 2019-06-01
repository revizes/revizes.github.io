~~~cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>

#define MAX_VERTICES    100

typedef struct {
    int w;
    int u;
    int v;
} element;

typedef struct {
    element data[MAX_VERTICES];
    int total;
} heap;

bool heap_init(heap *h)
{
    if (h == NULL) return false;

    memset((void *) h->data, 0x0, sizeof(element) * MAX_VERTICES);
    h->total = 0;

    return 0;
}

bool heap_insert(heap *h, element e)
{
    int current;
    if (h == NULL || (h->total + 1) >= MAX_VERTICES) return false;

    current = ++(h->total);

    while (current > 1) {
        if (e.w < h->data[current / 2].w) {
            h->data[current] = h->data[current / 2];
            current = current / 2;
        } else {
            break;
        }
    }

    h->data[current] = e;

    return true;
}

bool heap_delete(heap *h, element *e)
{
    int current, child;
    element tmp;

    if (h == NULL || h->total < 1) return false;

    *e = h->data[1];
    tmp = h->data[(h->total)--];
    current = 1;
    child = current * 2;

    while (child <= h->total) {
        if (child < h->total)
            if (h->data[child].w > h->data[child + 1].w)
                child = child + 1;

        if (tmp.w > h->data[child].w)
            h->data[current] = h->data[child];

        current = child;
        child *= 2;
    }

    h->data[current] = tmp;

    return true;
}

bool heap_deinit(heap *h)
{
    if (h == NULL) return false;

    h->total = 0;

    return true;
}

int parent[MAX_VERTICES];
int num[MAX_VERTICES];

bool init_union(int n)
{
    int i;

    for (i = 0; i < n; i++) {
        parent[i] = -1;
        num[i] = 1;
    }

    return true;
}

int union_find(int v)
{
    int p, s, i;

    for (i = v; (p = parent[i]) != -1; i = p)
        ;
    s = i;

    for (i = v; (p = parent[i]) != -1; i = p) {
        parent[i] = s;
    }

    return s;
}

int union_set(int u, int v)
{
    if (num[u] > num[v]) {
        parent[v] = u;
        num[u] += num[v];
    } else {
        parent[u] = v;
        num[v] += num[u];
    }
}

void insert_heap_edge(heap *h, int u, int v, int w)
{
    element e;

    e.u = u;
    e.v = v;
    e.w = w;

    heap_insert(h, e);
}

void kruscal(int n)
{
    int accepted = 0;
    element e;
    heap mheap;
    int uset, vset;

    heap_init(&mheap);

    insert_heap_edge(&mheap, 0, 1, 29);
    insert_heap_edge(&mheap, 1, 2, 16);
    insert_heap_edge(&mheap, 2, 3, 12);
    insert_heap_edge(&mheap, 3, 4, 22);
    insert_heap_edge(&mheap, 4, 5, 27);
    insert_heap_edge(&mheap, 5, 0, 10);
    insert_heap_edge(&mheap, 6, 1, 15);
    insert_heap_edge(&mheap, 6, 3, 18);
    insert_heap_edge(&mheap, 6, 4, 25);

    init_union(n);

    while (accepted != n - 1) {
        if (!heap_delete(&mheap, &e)) {
            printf("something wrong\n");
            break;
        }

        uset = union_find(e.u);
        vset = union_find(e.v);
            
        if (uset != vset) {
            printf("(%d, %d) %d\n", e.u, e.v, e.w);
            accepted++;
            union_set(e.u, e.v);
        }
    }

    heap_deinit(&mheap);
}


int main(void)
{
    kruscal(7);

    return 0;
}
~~~
