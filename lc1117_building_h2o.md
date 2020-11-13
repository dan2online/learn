***1117. Building H2O***

https://leetcode.com/problems/building-h2o/

```python
class H2O:
    def __init__(self):
        self.hlock = threading.Lock()
        self.olock = threading.Lock()
        self.olock.acquire()
        self.h_num = 0


    def hydrogen(self, releaseHydrogen: 'Callable[[], None]') -> None:
        self.hlock.acquire()
        # releaseHydrogen() outputs "H". Do not change or remove this line.
        releaseHydrogen()
        self.h_num += 1
        if self.h_num == 2:
            self.olock.release()
            self.h_num = 0
        else:
            self.hlock.release()


    def oxygen(self, releaseOxygen: 'Callable[[], None]') -> None:
        self.olock.acquire()
        # releaseOxygen() outputs "O". Do not change or remove this line.
        releaseOxygen()
        self.hlock.release()
        

class H2O_2:
    def __init__(self):
        self.semH = threading.Semaphore(2)
        self.semO = threading.Semaphore(0)
        self.nH = 0

    def hydrogen(self, releaseHydrogen: 'Callable[[], None]') -> None:
        self.semH.acquire()
        # releaseHydrogen() outputs "H". Do not change or remove this line.
        releaseHydrogen()
        self.nH += 1
        if self.nH == 2:
            self.nH = 0
            self.semO.release()

    def oxygen(self, releaseOxygen: 'Callable[[], None]') -> None:
        self.semO.acquire()
        self.semH.release()
        self.semH.release()
        # releaseOxygen() outputs "O". Do not change or remove this line.
        releaseOxygen()
```

