OOP


## 1.1 Định nghĩa một class
- Thực hiện khai báo các thuộc tính trong hàm __init__(). Các hàm trong class bắt đầu bằng đối số **self** để tham chiếu đến đối tượng hiện tại, khởi tạo tương tự như các hàm bình thường.
```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def calulate_area(self):
        self.area = self.width * self.height
        return self.area

    def caculate_perimeter(self):
        return (self.width + self.height) * 2
```

### Khởi tạo một đối tượng(object) từ một Class đã tạo
- Gọi Class, truyền vào các giá trị tương ứng trong hàm __init__ của Class

```python
my_rec = Rectangle(3,4)

#class -> đối tượng -> thuộc tính
#                   -> phương thức(các chức năng của class)

#in ra các thuộc tính của đối tượng
print(my_rec.width)
print(my_rec.height)

#gọi phương thức của đối tượng
print(my_rec.calulate_area())
print(my_rec.caculate_perimeter())
```
## Chi tiết các hàm trong Class
- _ _ _init_ _ _(): phương thức khởi tạo, được gọi tự động khi một đối tượng(object) mới của Class được tạo ra.
```python
class my_class:
    def __init__(self, value):
        self.value = value

obj = my_class(10)
print(obj.value) # 10
```

- _ _ _str_ _ _(): để định nghĩa object đấy là gì, thường được sử dụng bởi ***print***.
```python
class my_class:
    def __init__(self, value):
        self.value = value
    
    def __str__(self):
        return f"value of class {self.value}"

obj = my_class(10)
print(obj) # value of calss 10
```

- _ _ _len_ _ _(): trả về độ dài của object, sử dụng hàm ***len***

```python
class my_class:
    def __init__(self, item):
        self.item = item
    
    def __str__(self):
        return len(self.item)

obj = my_class([10, 11, 12])
print(len(obj)) # 3
```

- _ _ _call_ _ _(): cho phép đối tượng có thể được gọi như một hàm
```python
class add:
    def __init__(self, value):
        self.value = value
    def __call__(self, x):
        return self.value + x

add_five = add(5)
print(add_five(10)) # 15
```