OOP

# 1. Class
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
## 1.2 Chi tiết các hàm trong Class
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

# 2. OOP

## 2.1 Inheritance(tính kế thừa)
Cho phép một class có thể kế thừa các thuộc tính(attributes) và phương thức(methods) của một lớp khác.

![](asset/image.png)

Khi định nghĩa class con thì truyền vào class cha luôn. Sử dụng ***super()*** để gọi phương thức __init() của class cha.

```python
class cha:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(f"ten cha {self.name}")

class con(cha):
    def __init__(self, name, age):
        super().__init__(name)
        self.age = age
    def display(self):
        super().display()
        print(f"tuoi con {self.age}")

con = con("khanh", 22)
con.display() 

#ten cha khanh
#tuoi con 22
```

### Access modifiers
Kiểm soát mức độ truy cập và sử đổi các thuộc tính(attributes) và phương thức(method) của một class.

a. Public member 

Mặc định các thuộc tính và phương thức đều là public

```python
class my_class:
    def __init__(self, value):
        self.value = value

    def display(self):
        print(self.value)

obj = my_class(10)
print(obj.value) # truy cập thuộc tính công khai
obj.display # gọi phương thức công khai
```

b. Protect member

Chỉ nên được truy cập bên trong class và các lớp con của nó. Sử dụng dấu _ trước tên của thuộc tính hoặc phương thức

```python
class Class: 
    def __init__(self, value):
        self.value = value
    def _display(self):  # protect method
        print(self._value)

class subClass(Class):
    def show(self):
        self._display() # truy cập phương thức được bảo vệ từ lớp con

obj = subClass(20)
obj.show() # 20
```

c. Private members

Chỉ được truy cập bên trong class nơi chúng được định nghĩa. Sử dụng 2 dấu __ trước tên của thuộc tính hoặc phương thức

```python
class Class:
    def __init__(self, value):
        self.__value = value # private attribute

    def __display(self): # private method
        print(self.__value)

    def public_method(self):
        self.__display() # truy cập phương thức riêng tư từ bên trong class

obj = Class(30)
obj.public_method() # 30
print(obj.__value) # Error: AttributError
obj.__display() # Error:: MethodError
```

## 2.2 Override

Cho phép lớp con triển khai cụ thể của một phương thức đã được định nghĩa trong lớp cha. Cho phép ghi đè thay đổi hoặc mở rộng hành vi của phương thức kế thừa từ lớp cha trong lớp con

\- Cần định nghĩa lại phương thức đó cùng với tên và tham số trong lớp con

```python
# display() được ghi đè ở subclass
class cha:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(f"ten cha {self.name}")

class con(cha):
    def __init__(self, name, age):
        super().__init__(name)
        self.age = age
    def display(self):
        print(f"ten cua con {self.age}")
        print(f"tuoi con {self.age}")

con = con("khanh", 22)
con.display()  
# ten cua con khanh
# tuoi con 22
```

### Các loại kế thừa

a. Single Inheritance

Là một lớp con kế thừa từ 1 lớp cha duy nhất
```
   cha 
    ^
    |
   con
```

```python
class cha:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(f"ten cha {self.name}")

class con(cha):
    def __init__(self, name, age):
        super().__init__(name)
        self.age = age
    def display(self):
        super().display()
        print(f"tuoi con {self.age}")

con = con("khanh", 22)
con.display() 

#ten cha khanh
#tuoi con 22
```

b. Multiple Inheritance

Là một lớp con kế thừa từ nhiều lớp cha

```
cha1         cha2
      \    /
        con
```

```python
class cha1:
    def __init__(self):
        self.str1 = "cha1"
        print("khoi tao cha1")

class cha2:
    def __inti__(self):
        self.str2 = "cha2"
        print("khoi tao cha2")

class con(cha1, cha2):
    def __init__(self):
        cha1.__init(self)
        cha2.__init(self)
        print("khoi tao con")
    def display(self):
        print(self.str1, self.str2)

obj = con()
obj.display()

# khoi tao cha1
# khoi tao cha2
# khoi tao con
# cha1 cha2
```

c. Multilevel Inheritance(Kế thừa đa cấp)

Là lớp con kế thừa từ lớp cha, nhưng lớp cha kế thừa từ ông

```python
class ong:
    def __init__(self, ten_ong):
        self.ten_ong = ten_ong
    def display_ong(self):
        print(f"ten cua ong {self.ten_ong}")

class cha(ong):
    def __init__(self,ten_ong, ten_cha):
        super().__init__(ten_ong)
        self.ten_cha = ten_cha
    def display_cha(self):
        print(f"ten cua cha {self.ten_cha}")

class con(cha):
    def __init__(self, ten_ong, ten_cha, ten_con):
        super().__init__(ten_ong, ten_cha)
        self.ten_con = ten_con
    def display_con(self):
        print(f"ten cua con {self.ten_con}")

obj = con("tuong", "tien", "khanh")
obj.ten_ong() # ten cua ong tuong
obj.ten_cha() # ten cua cha tien
obj.ten_con() # ten cua con khanh
```

d. Hierarchical Inheritance(Kế thừa phân cấp)

Là có nhiều hơn 1 lớp kế thừa từ lớp cha

```
    cha
  /     \
con1    con2
```

```python
class cha:
    def __init__(self, ten_cha):
        self.ten_cha = ten_cha
    def display_cha(self):
        print(f"ten cua ong {self.ten_cha}")

class con1(cha):
    def __init__(self, ten_cha, ten_con1):
        super().__init__(ten_cha)
        self.ten_con1 = ten_con1
    def display_con1(self):
        print(f"ten cua con1 {self.ten_con1}")

class con2(cha):
    def __init__(self, ten_cha, ten_con2):
        super().__init__(ten_cha)
        self.ten_con2 = ten_con2
    def display_con1(self):
        print(f"ten cua con2 {self.ten_con2}")

con1 = con1("tien", "khanh")
con2 = con2("tien", "nhung")

con1.display_con1() #khanh
con2.display_con2() #nhung 
```