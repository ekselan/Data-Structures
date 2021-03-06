## Class III (Part I)

`BSTNode()` `insert()` method:
```py
def insert(self, value):
        """
        Insert the given value into the tree
        """
        # compare the input value with the value of the Node
        # if value < Node's value
        if value < self.value:
            # we need to go left
            # if we see there is no left child,
            if self.left is None:
                # then we can wrap the value in a BSTNode and
                # park it
                self.left = BSTNode(value)
            # otherwise there is a child
            else:
                # call the left child's `insert` method
                self.left.insert(value)
        # otherwise, value >= Node's value
        if value >= self.value:
            # we need to go right
            # if we see there is no right child,
            if self.right is None:
                # then we can wrap the value in a BSTNode and
                # park it
                self.right = BSTNode(value)
            # otherwise there is a child
            else:
                # call the right child's `insert` method
                self.right.insert(value)
```
---
`BSTNode()` `contains()` method:
```py
def contains(self, target):
        """
        Return True if the tree contains the value
        False if it does not
        """
        # Compare input value with value of the node
        # if value == Node's value
        if target == self.value:
            # return True
            return True
        else:
            # if value < Node's value
            if target < self.value:
                # if there is no right child
                if self.left is None:
                    # tree does not contain value
                    return False
                else:
                    # call the left child's `contains` method
                    return self.left.contains(target)
            # if value > Node's value
            if target > self.value:
                # if there is no right child
                if self.right is None:
                    # tree does not contain value
                    return False
                else:
                    # call the right child's `contains` method
                    return self.right.contains(target)
```
---
`BSTNode()` `get_max()` method:
```py
def get_max(self):
        """
        Return the maximum value found in the tree
        """
        # Inspect root node
        max_val = self.value
        # Check for children
        if self.right is None:
            return max_val
        else:
            # Check if right child value is < Node value
            if self.right.value < max_val:
                return max_val
            else:
                max_val = self.right.value
                # call the right child's `get_max` method
                return self.right.get_max()
```
---
`BSTNode()` `for_each()` method:
```py
def for_each(self, fn):
        """
        Call the function `fn` on the value of each node
        """
        # fn(root.value)
        # Start with root (no children)
        if self.left is None and self.right is None:
            return fn(self.value)
        else:
            # Handle both sides when not None
            if self.left is not None and self.right is not None:
                return fn(self.value), self.left.for_each(
                    fn), self.right.for_each(fn)
            # Hande right side
            if self.right is not None and self.left is None:
                return fn(self.value), self.right.for_each(fn)
            # Handle left sides
            if self.left is not None and self.right is None:
                return fn(self.value), self.left.for_each(fn)
```
---

## Class IV (Part II)

`BSTNode()` `in_order_print()` method:
```py
def in_order_print(self, node):
    """
    Print all the values in order from low to high
    Hint:  Use a recursive, depth first traversal
    """
    # Use a stack to guide traversal
    stack = []
    stack.append(self)

    vals = set()

    # so long as our stack has nodes in it
    # there's more nodes to traverse
    while len(stack) > 0:
        # pop the top node from the stack
        current = stack.pop()
        vals.add(current.value)

        # add the current node's right child first (for left to right
        # order)
        if current.right:
            vals.add(current.right.value)
            stack.append(current.right)

        # add the current node's left child
        if current.left:
            vals.add(current.left.value)
            stack.append(current.left)

    # Need to print each value from low to high
    for i in sorted(list(vals)):
        print(i)
```
---
`BSTNode()` `bft_print()` method:
```py
def bft_print(self, node):
    from collections import deque
    """
    Print the value of every node, starting with the
    given node, in an iterative breadth first traversal.
    layers, FIFO
    """
    # Use a queue to guide traversal
    queue = deque()
    queue.append(self)

    vals = []
    vals.append(self.value)

    # so long as our stack has nodes in it
    # there's more nodes to traverse
    while len(queue) > 0:
        # pop the top node from the stack
        current = queue.popleft()

        # check for children

        # add the current node's right child first (for left to right
        # order)
        if current.right:  # and current.left is None:
            vals.append(current.right.value)
            queue.append(current.right)

        # add the current node's left child
        if current.left:  # and current.right is None:
            vals.append(current.left.value)
            queue.append(current.left)

    # Need to print each value
    for i in vals:
        print(i)
```
---
`BSTNode()` `dft_print()` method:
```py
def dft_print(self, node):
    """
    Print the value of every node, starting with the
    given node, in an iterative depth first traversal.
    LIFO
    """
    # Use a stack to guide traversal
    stack = []
    stack.append(self)

    vals = []
    # vals.append(self.value)

    # so long as our stack has nodes in it
    # there's more nodes to traverse
    while len(stack) > 0:
        # pop the top node from the stack
        current = stack.pop()

        # check for children

        # add the current node's right child first (for left to right
        # order)
        if current.right:  # and current.left is None:
            # vals.append(current.right.value)
            stack.append(current.right)

        # add the current node's left child
        if current.left:  # and current.right is None:
            # vals.append(current.left.value)
            stack.append(current.left)

        vals.append(current.value)

    # Need to print each value
    for i in vals:
        print(i)
```
