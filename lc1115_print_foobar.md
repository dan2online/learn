

***1115. Print FooBar Alternately***

https://leetcode.com/problems/print-foobar-alternately/

```Python
class FooBar:
    def __init__(self, n):
        self.n = n
        self.flag = 1

    def foo(self, printFoo: 'Callable[[], None]') -> None:
        
        for i in range(self.n):
            while self.flag != 1:
                time.sleep(0.005)
            
            # printFoo() outputs "foo". Do not change or remove this line.
            printFoo()
            
            self.flag = 2

    def bar(self, printBar: 'Callable[[], None]') -> None:
        
        for i in range(self.n):
            while self.flag != 2:
                time.sleep(0.005)
            # printBar() outputs "bar". Do not change or remove this line.
            printBar()
            
            self.flag = 1
            


```



```python
class FooBar:
    def __init__(self, n):
        self.n = n
        self.foo_lock = threading.Lock()
        self.bar_lock = threading.Lock()
        self.bar_lock.acquire()


    def foo(self, printFoo: 'Callable[[], None]') -> None:
        
        for i in range(self.n):
            self.foo_lock.acquire()
            
            # printFoo() outputs "foo". Do not change or remove this line.
            printFoo()
            
            self.bar_lock.release()


    def bar(self, printBar: 'Callable[[], None]') -> None:
        
        for i in range(self.n):
            self.bar_lock.acquire()
            # printBar() outputs "bar". Do not change or remove this line.
            printBar()
            
            self.foo_lock.release()
```

