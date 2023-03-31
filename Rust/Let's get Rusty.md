> Stack is of fixed size, its size is calculated at compile time. So it cannot grow or shrink

>When you allocate memory space on the heap, the program have to seach for empty memory on the heap and return a pointer to it to your variable thats stored on the stack(wich is costly in terms of performance)

>so accessing memory in the stack is faster than on the heap(cause you have to follow the pointer)

