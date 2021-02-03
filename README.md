# python-kill-thread

```python
import ctypes
import threading
import time


def kill_thread(thread):
    """
    thread: a threading.Thread object
    """
    thread_id = thread.ident
    res = ctypes.pythonapi.PyThreadState_SetAsyncExc(thread_id, ctypes.py_object(SystemExit))
    if res > 1:
        ctypes.pythonapi.PyThreadState_SetAsyncExc(thread_id, 0)
        print('Exception raise failure')

def func():
    while True:
        print('thread running')


t1 = threading.Thread(target=func)
t1.start()
time.sleep(2)
kill_thread(t1)
if not t1.is_alive():
    print('thread killed')
```
