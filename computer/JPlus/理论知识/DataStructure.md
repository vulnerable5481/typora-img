# 基础篇



## 前置基础





## 链表







## 堆，栈



### 1.简单应用

<font color='red'>注意：Java堆栈Stack类已经过时，Java官方推荐使用Deque替代Stack使用。Deque堆栈操作方法：push()、pop()、peek()。</font>

```
双端队列：Deque<TreeNode> stack = new ArrayDeque<>();
栈: Queue queue = new LinkedList<>();
```











## 二叉树

### 1.前中后

递归版本	

```
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        tree(root,res);
        return res;
    }
    public void tree(TreeNode cur,List<Integer> res){
        if(cur == null) return;
        tree(cur.left,res);
        res.add(cur.val);
        tree(cur.right,res);
    }
```

中序遍历:   

```
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        if (root == null) {
            return list;
        }
        Deque<TreeNode> stack = new ArrayDeque<>();
        while (root != null || !stack.isEmpty()) {
            if(root != null){
                stack.push(root);
                root = root.left;
            }else{
                root = stack.pop();
                list.add(root.val);
                root = root.right;
            }

        }
        return list;
    }
```

前序遍历：

```
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root == null)return res;
        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(root);
        while(!stack.isEmpty()){
            root = stack.pop();
            res.add(root.val);
            if(root.right != null){
                stack.push(root.right);
            }
            if(root.left != null){
                stack.push(root.left);
            }
        }
        return res;
    }
```

后序遍历:

```
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root == null) return res;
        Deque<TreeNode> stack = new ArrayDeque<>();
        Deque<TreeNode> stack2 = new ArrayDeque<>();
        stack.push(root);
        while(!stack.isEmpty()){
            root = stack.pop();
            stack2.push(root);
            if(root.left != null){
                stack.push(root.left);
            }
            if(root.right != null){
                stack.push(root.right);
            }

        }
        while(!stack2.isEmpty()){
            root = stack2.pop();
            res.add(root.val);
        }
        return res;
    }
```





































## 图









## 

















































































































































































































































































