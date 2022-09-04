### 实现要素
- 符合RAII设计，离开作用域后自动释放资源
- 默认构造、拷贝构造、赋值运算符的实现
- *、->运算符实现
- 引用计数的实现
- 多线程安全

### 简单实现I（不考虑多线程安全）
```
template <class T>
class MySharedPtr {
public:
  MySharedPtr(T* ptr = nullptr) {
    _ptr = ptr;
    _count = new int(0);
    if (_ptr != nullptr) {
      *_count = 1;
    }
  }

  MySharedPtr(const MySharedPtr& rhs) {
    _ptr = rhs._ptr;
    _count = rhs._count;
    *_count += 1;
  }

  MySharedPtr& operator=(const MySharedPtr& rhs) {
    if (_ptr == rhs._ptr) { // 考虑自身拷贝的情况
      return *this;
    }
    *_count -= 1;
    destroy(); // 先释放资源，如果引用计数为0
    _count = rhs._count;
    _ptr = rhs._ptr;
    *_count += 1;
    return *this;
  }

  ~MySharedPtr() {
    *_count -= 1;
    destroy();
  }

  T& operator*() {
    return *_ptr;
  }

  T* operator->() {
    return _ptr;
  }

private:
  void destroy() {
    if (*_count == 0) {
      delete _ptr;
      delete _count;
    }
  }

private:
  int* _count;
  T* _ptr;
};
```

### 简单实现II（多线程安全）
```
// TODO
```
