# -data-structure-exercises   محمدرضاکشاورز
تمرین‌های درس ساختمان داده به زبان پایتون

# ================= doubly linked list =================

class dnode():
    def __init__(self , x):
        self.Data = x
        self.next = None
        self.back = None


class dlinked_list :
    def __init__(self):
        self.head = None

    def del_after(self , x):
        if self.head is None:
            print("error")
            return
        c = self.head
        while c:
            if c.Data == x:
                if c.next :
                    a = c.next
                    c.next = a.next
                    if a.next:
                        a.next.back = c
                    del a
                    return
                print("error 1")
                return
            c = c.next
        print("not found")

    def del_x(self , x):
        if self.head is None:
            print("error")
            return
        c = self.head
        while c:
            if c.Data == x:
                if c.next is None:
                    self.del_last()
                    return
                if c.back:
                    c.back.next = c.next
                if c.next:
                    c.next.back = c.back
                del c
                return
            c = c.next
        print("not found")


############################################################

class dnode():
    def __init__(self , x):
        self.Data = x
        self.next = None
        self.back = None


class dlinked_list :
    def __init__(self):
        self.head = None

    def ins_frist(self , x):
        a = dnode(x)
        if self.head:
            a.next = self.head
            self.head.back = a
        self.head = a

    def ins_last(self , x):
        if self.head is None:
            self.ins_frist(x)
            return
        c = self.head
        while c.next:
            c = c.next
        a = dnode(x)
        c.next = a
        a.back = c

    def ins_after(self , x ,y):
        if self.head is None:
            print("error")
            return
        c = self.head
        while c :
            if c.Data == x:
                if c.next is None:
                    self.ins_last(y)
                    return
                a = dnode(y)
                a.next = c.next
                c.next.back = a
                c.next = a
                a.back = c
                return
            c = c.next
        print("not found")

    def ins_befor(self , x , y):
        if self.head is None:
            print("error")
            return
        c = self.head
        while c:
            if c.Data == x:
                if c.back is None:
                    self.ins_frist(y)
                    return
                a = dnode(y)
                a.next = c
                a.back = c.back
                c.back.next = a
                c.back = a
                return
            c = c.next
        print("not found")

    def del_first(self):
        if self.head is None:
            print("error")
            return
        self.head = self.head.next
        if self.head:
            self.head.back = None

    def del_last(self):
        if self.head is None:
            print("error")
            return
        c = self.head
        while c.next:
            c = c.next
        if c.back is None:
            self.head = None
        else:
            c.back.next = None

    def del_befor(self , x):
        if self.head is None or self.head.Data == x:
            print("error")
            return
        c = self.head
        while c :
            if c.Data == x:
                a = c.back
                c.back = a.back
                if a.back:
                    a.back.next = c
                del a
                return
            c = c.next
        print("x not found")


# ================= singly linked list =================

class node :
    def __init__(self , d):
        self.Data = d
        self.next = None


class linked_list :
    def __init__(self):
        self.head = None

    def insert_frist(self , x):
        a = node(x)
        a.next = self.head
        self.head = a

    def insert_last(self , x):
        if self.head is None:
            self.head = node(x)
            return
        c = self.head
        while c.next:
            c = c.next 
        c.next = node(x)

    def insert_after(self , x, y):
        if self.head is None:
            print("list is empty")
            return
        c = self.head
        while c:
            if c.Data == x:
                a = node(y)
                a.next = c.next
                c.next = a
                return
            c = c.next
        print("not found")

    def insert_befor(self , x, y):
        if self.head is None:
            print("list is empty")
            return
        if self.head.Data == x:
            self.insert_frist(y)
            return
        c = self.head
        while c.next:
            if c.next.Data == x:
                a = node(y)
                a.next = c.next
                c.next = a
                return
            c = c.next
        print("not found")


# ================= graph =================

def BFS(graph , start):
    queue = [start]
    visited = {start}
    while queue:
        vertex = queue.pop(0)
        for ne in graph[vertex]:
            if ne not in visited:
                visited.add(ne)
                queue.append(ne)
    return visited


def DFS(graph , start , visited):
    visited[start] = True
    for ne in graph[start]:
        if not visited[ne]:
            DFS(graph , ne , visited)


# ================= sorting =================

def Bubble(A):
    for i in range(len(A)-1):
        for j in range(len(A)-1-i):
            if A[j] > A[j+1]:
                A[j], A[j+1] = A[j+1] , A[j]


# ================= tree =================

class Tree_Node :
    def __init__(self , x):
        self.Data = x
        self.Lchild = None
        self.Rchild = None


def Count_leaves(root):
    if root is None:
        return 0
    if root.Lchild is None and root.Rchild is None:
        return 1
    return Count_leaves(root.Lchild) + Count_leaves(root.Rchild)


def Count_1Deg(root):
    if root is None:
        return 0
    if (root.Lchild is None) ^ (root.Rchild is None):
        return 1
    return Count_1Deg(root.Lchild) + Count_1Deg(root.Rchild)


def Count_2Deg (root):
    if root is None:
        return 0
    if root.Lchild and root.Rchild:
        return 1
    return Count_2Deg(root.Lchild) + Count_2Deg(root.Rchild)


def sum_Tree(root):
    if root is None:
        return 0
    return root.Data + sum_Tree(root.Lchild) + sum_Tree(root.Rchild)


def Count(root):
    if root is None:
        return 0
    return 1 + Count(root.Lchild) + Count(root.Rchild)


def search(root , t):
    if root is None:
        return False
    if root.Data == t:
        return True
    return search(root.Lchild , t) or search(root.Rchild , t)


def max_t(root):
    if root is None:
        return float("-inf")
    return max(root.Data , max_t(root.Lchild) , max_t(root.Rchild))


# ================= stack =================

class stack : 
    def __init__(self , limit = 1000):
        self.st=[]
        self.lim = limit

    def push(self , x):
        if len(self.st) >= self.lim:
            print("stack is full")
            return
        self.st.append(x)

    def pop(self):
        if len(self.st) == 0 :
            print("stack is empty")
            return
        return self.st.pop()

    def peek(self):
        if len(self.st) == 0 :
            print("stack is empty")
            return
        return self.st[-1]

    def find(self,x):
        for i in range(len(self.st)):
            if self.st[i] == x :
                print(i)


# ================= fibonacci =================

def fib(n):
    if n==1 or n==2:
        return 1
    return fib(n-1) + fib(n-2)

