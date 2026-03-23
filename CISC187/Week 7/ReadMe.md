# Reflection Questions

Answer the following questions in your README.

1. Why is a linked list efficient for stack implementation?

A linked list is efficient specially for stack implementation because it allows for us to both push and pop at the head. That requires way less steps then pushing at the top and popping from the bottom. It's size is also dynamic so that is also one less thing that you have to account for.

2. What is the time complexity of push and pop operations?

Both operations for push and pop are O(1) because we are able to push and pop at the head, there are no extra steps required. This allows us to not traverse the list which does not increase the time cost.

3. What happens if memory is not deallocated after pop?

If memoery is not deallocated, then left over memory stays within the list. This can lead to more memory consumption and eventually causing corruption if the program continues to push more data to the list. It is very important to reset or delete.

4. Compare a stack implemented with an array versus a linked list.

The biggest difference between a stack implemented with an array versus a linked list is their size. While the stack has a fixed size, a linked list has no size limit. So stacks can be overflowed if too many elements are added wheras with proper implementation, the linked list won't but it will use up additional unaccounted for memory.

---
