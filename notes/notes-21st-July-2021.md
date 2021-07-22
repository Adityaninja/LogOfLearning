# 21st July

## Find the least common ancestor (LCA)

- Finding paths and then finding the first element which is not common
``` python
def find_path_approach(self, root, p, q):
    path1 = self.get_path(root, p)
    path2 = self.get_path(root, q)
    x = self.find_intersection(path1, path2)
    return x

def find_intersection(self, path1, path2):
    i = 0
    path_to_consider = path1 if len(path1) < len(path2) else path2
    while i < len(path_to_consider) and path1[i] == path2[i]:
        i += 1

    if i == len(path_to_consider):
        return path_to_consider[-1]

    return path_to_consider[i]

def get_path(self, root, p):
    path = self._traverse(root, p, [root])
    return path

def _traverse(self, node, target, path):
    if node is None:
        return None

    if node.val == target.val:
        return path[:]

    left_result = self._traverse(node.left, target, path + [node.left])
    if left_result:
        return left_result

    right_result = self._traverse(node.right, target, path + [node.right])
    if right_result:
        return right_result

    return None
```

- Single traversal approach. The core of it is that even if you do not know the element you are returning
  the lca, you know that the check left_result != None and right_result != None IS the LCA.

``` python
def single_traversal(self, node, p, q):
    if node.val == p.val or node.val == q.val:
        return node

    left_node = None
    right_node = None
    if node.left is not None:
        left_node = self.single_traversal(node.left, p, q)

    if node.right is not None:
        right_node = self.single_traversal(node.right, p, q)

    if left_node and right_node:
        return node

    return left_node if left_node is not None else right_node
```
