test
这个有用吗
学习python时的一些代码
#!/usr/bin/env python 
# -*- coding:utf-8 -*-

""" a test module """

import sys
import math
import re
from collections import Iterable
from functools import reduce
from operator import itemgetter
import functools

def my_abs(x):
    if not isinstance(x, (int, float)):
        return TypeError('bad operand type')
    if x > 0:
        return x
    else:
        return -x

def move(x, y, step, angle=0):
    nx = x + step * math.cos(angle)
    ny = y - step * math.sin(angle)
    return nx, ny

def quadratic(a, b, c):
    if not isinstance(a,(int, float)) or not isinstance(b,(int,float)) or not isinstance(c,(int,float)):
        return TypeError('Bad operand type')
    if a == 0:
        return TypeError('a can\'t equal to 0')
    delta = math.pow(b, 2)-4*a*c
    if delta < 0:
        return "无实根"
    x1 = (-b + math.sqrt(delta)) / (2 * a)
    x2 = (-b - math.sqrt(delta)) / (2 * a)
    return x1, x2

def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s

def add_end(L=None):
    if L is None:
        L = []
    L.append('END')
    return L

def calc(*numbers):
    # 可变参数
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum

def person(name, age, **kw):
    # 关键字参数
    print('name:', name, 'age:', age, 'other:', kw)
def person1(name, age, *, city, job):
    # 和关键字参数**kw不同，命名关键字参数需要一个特殊分隔符*，*后面的参数被视为命名关键字参数。
    print(name, age, city, job)
def person2(name, age, *args, city, job):
    # 如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符*了
    print(name, age, args, city, job)

# 尾递归
def fact_iter(num, product):
    if num == 1:
        return product
    return fact_iter(num - 1, num * product)
def fact(n):
    return fact_iter(n, 1)
# 汉诺塔
def hnt(n,a,b,c):
    if n ==1:
        print('move', a, '-->', c)
    else:
        hnt(n-1, a, c, b)
        hnt(1, a, b, c)
        hnt(n-1, b, a, c)

def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'

# 杨辉三角
def triangles():
    yield [1]  # 打印第一行
    yield [1, 1]   # 打印第二行
    L0 = [1, 1]   #
    i = 2
    while i < 10:
        L1 = [1]  # L1是下一行的列表，下一行的第一个是1
        L2 = [L0[j] + L0[j+1] for j in range(len(L0) - 1)]  # 生成下一行的其他列表
        L1.extend(L2)
        L1.append(1)  # L1的最后一个是1
        L0 = L1
        yield L1  # 生成剩余的几行
# 既然变量可以指向函数，函数的参数能接收变量，
# 那么一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。
def add(x, y, f):
    return f(x) + f(y)
def add1(x, y):
    return x+y
def fn(x, y):
    return x*10+y

def normalize(name):
    return name.capitalize()

def prod(L):
    def sum(x, y):
        return x*y
    return reduce(sum, L)

# 当一个函数返回了一个函数后，其内部的局部变量还被新函数引用，所以，闭包用起来简单，实现起来可不容易。
# # 另一个需要注意的问题是，返回的函数并没有立刻执行，而是直到调用了f()才执行
def createCounter():
    s = [0]
    def counter():
        s[0] = s[0]+1
        return s[0]
    return counter

if __name__ == '__main__':
    print("hello world!")
    print("10+200 =", 100 + 200)
    print('The quick brown fox', 'jumps over', 'the lazy dog')
    '''
    name = input()  # 输入
    print("my name is ", name)
    name = input('please enter your name: ')
    print('hello,', name)
    print("1024 * 768 = ", 1024 * 768 )
   
    a = 100
    if a > 0:
        print(a)
    else:
        print(-a)
    print(0xff00)
    print(0xa5b4c3d2)
    print(1.2e5)
    print('I\'m \n"ok"!')
    print('\\\n\\')
    print('\\\t\\')
    print(r'\\\t\\')
    '''
    print('''line\nline2''')
    print(r'''hello,\n world''')
    '''
    print((3 < 5) and not (3 > 5))
    age = 12
    if age >= 18:
        print("adult")
    elif age >= 16:
        print("teenager")
    else:
        print("kid")
    print(11 / 3, 10 % 3, 11 // 3)
    print("'hello, \\'world\\''")
    '''
    print("r'''hello,\n\"bart\"'''")
    '''
    print(ord('我'))
    print(chr(25105))
    print('\u4e2d\u6587')
    print('ABC'.encode('ascii'))
    print('中文'.encode('utf-8'))
    print('Hello, %s' % 'world')
    print('Hi, %s, you have $%d.' % ('Michael', 1000000))
    print('%2d-%02d' % (3, 1))
    print('%.2f' % 3.1415926)
    print('growth rate: %d %%' % 7)
    print('Hello, {0}, 成绩提升了 {1:.2f}%'.format('小明', (85 - 72) / 72 * 100))
    classname = ['xg1501', 'xg1502']
    print(classname, len(classname))
    classname.append('xg1601')
    print(classname, len(classname))
    classname.insert(1, 'xg1602')
    classname.pop()
    print(classname, len(classname))
    t = (1, 2, 3)
    print(t)
    L = [
        ['Apple', 'Google', 'Microsoft'],
        ['Java', 'Python', 'Ruby', 'PHP'],
        ['Adam', 'Bart', 'Lisa']
    ]
    print(L[0][0], L[1][1], L[2][2])
    height = 1.60
    weight = 60.5
    bmi = weight / pow(height, 2)
    print(bmi)
    if bmi > 32:
        print("严重肥胖")
    elif bmi > 28:
        print("肥胖")
    elif bmi > 25:
        print("过重")
    elif bmi > 18.5:
        print("正常")
    else:
        print("过轻")
    names = ['Michael', 'Bob', 'Tracy']
    for name in names:
        print(name)
    print(names)
    s = 0
    for x in range(101):
        s = s + x
    print(s)
    sum = 0
    n = 99
    while n > 0:
        sum = sum + n
        n = n - 2
    print(sum)
    L = ['Bart', 'Lisa', 'Adam']
    for name in L:
        print("hello,", name)
    n = 1
    while n <= 100:
        if n > 10:
            break
        print(n)
        n = n + 1
    print('END')
    n = 0
    while n < 10:
        n = n + 1
        if n % 2 == 0:  # 如果n是偶数，执行continue语句
            continue  # continue语句会直接继续下一轮循环，后续的print()语句不会执行
        print(n)
    d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
    print(d['Tracy'])
    d['Adam'] = 67
    print(d['Adam'])
    print(d.get('cc', -1))
    print('cc' in d)
    print(d.pop('Bob'))
    print(d)
    s = set([1, 2, 3, 1, 1])
    print(s)
    s.add(4)
    s.remove(1)
    print(s)
    s1 = set([1, 2, 3])
    s2 = set([4, 2, 3])
    print(s1 & s2)
    print(s1 | s2)
    a = [13, 12, 1, 2]
    a.sort()
    print(a)
    print(abs(-100))
    print(max(1, 3, 4, 6), min(1, 3, 5), int(13.2), float('12.34'), str(12.3), bool(""), hex(1000))
    print(my_abs('k'))
    print(move(100, 100, 60, math.pi/6))
    print('quadratic(2, 3, 1) =', quadratic(2, 3, 1))
    print('quadratic(1, 3, -4) =', quadratic(1, 3, -4))
    print(power(5), power(5, 2))
    print(add_end(), add_end())
    num = [1, 2, 3]
    print(calc(1, 2, 3), calc(*num))
    person('cc', 22)
    person('Bob', 35, city='Beijing')
    person('Adam', 45, gender='M', job='Engineer')
    extra = {'city': 'Beijing', 'job': 'Engineer'}
    person('Jack', 24, city=extra['city'], job=extra['job'])
    person('Jack', 24, **extra)
    # 命名关键字参数必须传入参数名，这和位置参数不同。如果没有传入参数名，调用将报错：
    # 参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数。
    person1('Jack', 24, city='Beijing', job='Engineer')
    print(fact(1), fact(10), fact(100))
    hnt(3, 'A', 'B', 'C')
    # 切片
    L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
    print(L[:3], L[4:3], L[-2:-1])
    l = list(range(100))
    print(l[:10:2], l[::5])
    for ch in 'ABC':
        print(ch)
    print(isinstance(123, Iterable), isinstance('qwe', Iterable))
    for i, value in enumerate(['A', 'B', 'C']):
        print(i, value)
    for x, y in [(1, 1), (2, 4), (3, 9)]:
        print(x, y)
    ls = [1, 2, 3, 4]
    t = (max(ls), min(ls))
    print(t)
    print([x * x for x in range(1, 11) if x % 2 == 0])
    print([m + n for m in 'avc' for n in 'er'])
    d = {'x': 'A', 'y': 'B', 'z': 'C'}
    for k, v in d.items():
        print(k, '=', v)
    L1 = ['Hello', 'World', 18, 'Apple', None]
    print([s.capitalize() for s in L1 if isinstance(s,str)])
    g = (x * x for x in range(10))
    for n in g:
        print(n)
    for n in fib(6):
        print(n)
    # 测试
    n = 0
    results = []
    for t in triangles():
        print(t)
        results.append(t)
        n = n + 1
        if n == 10:
            break
    if results == [
        [1],
        [1, 1],
        [1, 2, 1],
        [1, 3, 3, 1],
        [1, 4, 6, 4, 1],
        [1, 5, 10, 10, 5, 1],
        [1, 6, 15, 20, 15, 6, 1],
        [1, 7, 21, 35, 35, 21, 7, 1],
        [1, 8, 28, 56, 70, 56, 28, 8, 1],
        [1, 9, 36, 84, 126, 126, 84, 36, 9, 1]
    ]:
        print('测试通过!')
    else:
        print('测试失败!')
    '''
    # 编写高阶函数，就是让函数的参数能够接收别的函数。
    print(add(-5, 6, abs))
    # map()函数接收两个参数，一个是函数，一个是Iterable，
    # map将传入的函数依次作用到序列的每个元素，并把结果作为新的Iterator返回。
    m = map(abs, [-5, -4, 2])
    for n in m:
        print(n)
    print(reduce(add1, [1, 2, 3, 4]))
    print(sum([1, 2, 3, 4]))
    print(reduce(fn, [1, 2, 3, 4]))
    print(int('123')+1)
    L1 = ['adam', 'LISA', 'barT']
    L2 = list(map(normalize, L1))
    print(L2)
    print('3 * 5 * 7 * 9 =', prod([3, 5, 7, 9]))
    if prod([3, 5, 7, 9]) == 945:
        print('测试成功!')
    else:
        print('测试失败!')
    print(sorted([36, 5, -12, 9, -21]))
    print(sorted([36, 5, -12, 9, -21], key=abs))
    print(sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True))
    students = [('Bob', 75), ('Adam', 92), ('Bart', 66), ('Lisa', 88)]
    print(sorted(students, key=itemgetter(0)))
    print(sorted(students, key=lambda t: t[1]))
    print(sorted(students, key=itemgetter(1), reverse=True))
    # 测试
    counterA = createCounter()
    print(counterA(), counterA(), counterA(), counterA(), counterA())  # 1 2 3 4 5
    counterB = createCounter()
    if [counterB(), counterB(), counterB(), counterB()] == [1, 2, 3, 4]:
        print('测试通过!')
    else:
        print('测试失败!')

    # 偏函数
    # functools.partial的作用就是，把一个函数的某些参数给固定住（也就是设置默认值），
    # 返回一个新的函数，调用这个新函数会更简单。
    print(int('124', base=16))
    int2 = functools.partial(int, base=2)
    print(int2('1111100000'))
    # 模块
    args = sys.argv
    if len(args) == 1:
        print('Hello, world!')
    elif len(args) == 2:
        print('Hello, %s!' % args[1])
    else:
        print('Too many arguments!')
    try:
        print('try...')
        r = 10 / int('s')
        print('result:', r)
    except ValueError as e:
        print('ValueError:', e)
    except ZeroDivisionError as e:
        print('ZeroDivisionError:', e)
    else:
        print('no error!')
    finally:
        print('finally...')
    print('END')
    # 正则表达式
    print(re.match(r'^\d{3}\-\d{3,8}$', '010 12345'))
    print('a b  c'.split(' '))
    print(re.split(r'\s+', 'a b  c'))
    print(re.split(r'[\s\,]+', 'a,b, c  d'))
