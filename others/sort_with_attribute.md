# Problem
根据对象属性进行排序，例如给定Person对象，要求根据年龄或薪水进行排序。

```python
class Person:
    def __init__(self, name, age, salary):
        self.name = name
        self.age = age
        self.salary = salary

obj_list = [
    Person('juneys', 20, 3000),
    Person('sam', 20, 2000),
    Person('eddy', 22, 2500),
    Person('eagle', 25, 1000)
]

# 第一种方法
obj_list.sort(key=lambda x: x.salary, reverse=False)
print('method 1:')
for obj in obj_list:
    print(obj.name, obj.salary)

# 第二种方法
import operator
# 优先按年龄排序，再按薪水排序
cmpfun = operator.attrgetter('age', 'salary')
obj_list.sort(key=cmpfun, reverse=True)
print('method 2:')
for obj in obj_list:
    print(obj.name, obj.salary, obj.age)

```
