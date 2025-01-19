1. Abstraction (abstrakcja)
2. inheritance (dziedziczenie)
3. polymorphizm (polimorfizm)
4. Encapsulation ()


```python
employee1_name = "Mateusz"  
employee1_age = 30  
employee1_position = "Software Engineer"  
employee1_salary = 10000  
 
employee2_name = "Martyna"  
employee2_age = 35  
employee2_position = "Senior Python Developer"  
employee2_salary = 12000  

employee1 = ["Mateusz", 30, "Software Engineer", 10000]  
employee2 = ["Martyna", 35, "Senior Python Developer", 12000]  
name = lambda employee: employee[0]  
age = lambda employee: employee[1]  
position = lambda employee: employee[2]  
salary = lambda employee: employee[3]  

utrzymanie takich danych jest trudne  
  
  
employee1 = {  
    "name": "Mateusz",  
    "age": 30,  
    "position": "Software Engineer",  
    "salary": 10000,  
}
```
, przecinek na końcu ostatniego elementu to trailing comma


```python
def init_employee(name, age, position, salary):  
    return {  
        "name": name,  
        "age": age,  
        "position": position,  
        "salary": salary,  
    }  
  
employe3 = init_employee("Cezary", 34, "Frontend Developer", 8000)  
  
print(employe3)
```
potrzebuję 1000 python dev. wzorzec projektowy? fabryka + builder?

w paradygmacie oop chcemy trzymać dane, blisko funkcjonalności

```
def increase_salary(employee, percent):  
    employee["salary"] += employee["salary"] * (percent / 100) 

```  
 używa referencji do obiektu  
 łamie pure function

```
def employee_info(employee):  
    return f'{employee["name"]} is {employee["position"]} and earns {employee["salary"]
```

sprawdzanie drzewa dziedziczenia danej klasy
```python
int.__mro__

```
w przypadku int zachodzi wirtualne dziedziczenie (protokoły też są przez to robione)
co do zasady każdy int może być reprezentowany przez floata.

w py obiekty tworzy się za pomocą obiektu innego typu: type
można sprawdzić poprzez zmienna.__class__




s1.upper() postfix (używane w OOP)

len(s) - prefix (używane w paradygmacie fn)

w padygmacie fn to normalne że tworzysz helpery typu
```python
def upper(text)
	return text.upper()

```

```python
n = None
n.__class__.__class__
# type
n.__class__.__class__.__class__ (skoro Bóg stworzył wszystko, to co stworzyło Boga? odp: Bóg sam siebie stworzł.)
```


z technicznego pkt widzenia klasa to taki słownik, tylko dopakowany

```
class Employee:  
    pass  
  
e = Employee()  
print(e)
<__main__.Employee object at 0x7c183afc3b80>
```
dunder main to moduł
0x7c183afc3b80> to szesnastkowy zapis wskazujący na miejsce w pamięci gdzie znajduje się obiekt klasy

w momencie gdy robimy import moduły są one [[singletone]]

circular import: moduł a importuje moduł b a moduł b import a. nic się z tym nie da zrobić

dunder init zawsze się wykonuje podczas importowania czegokolwiek z package.
dunder init to nic innego jak dunder init z klasy, bo przecież package to obiekty
#### jeśłi importujemy cokolwiek z modułu, to moduł jest w całości wykonywany.
#### jeśłi w module są jeki kolwiek wywołania, to one się wywołują przy imporcie

po zaimportowaniu czegoś, jeśłi zaczniemy to modyfikować, to nic nie da ponowny import
bo nie da się dwukrotnie zaimportować tego samego modułu, bo już jest
 trzeba najpierw usunąć dany moduł i dopiero zaimportować ponownie


podczas tworzenia klasy wykonuje się najpierw dunder new i on tworzy obiekt, później wykonuje się dunder init. new i init można powiedzieć że są konstruktorem, choć właściwym konstruktorem jest new, init tylko inicjalizuje pola klasy

self to referencja do obiektu, który powstał z dunder new

poprzez dunder dict można pominąć wszystkie zabezpieczenia przed modyfikacją elementów w klasie

py w klasach do atrybutów pod spodem używa dunder dict

dunder repr służy do pokazania w jaki sposób została zrobiona instancja obiektu.
repr zwraca zawsze typy danych, tak jak się je tworzy

dunder metody to special metods (już nie python features)
[https://docs.python.org/3/reference/datamodel.html#special-methods](https://docs.python.org/3/reference/datamodel.html#special-methods)

jeśli inicjujemy wartość poza dunder init istnieje ryzyko, że dane pole nie zostanie wywołane i nie będzie istnieć, a ktoś będzie chciał go użyć

metaklasa property jest dataobjecrt descriptorem

```python
class Employee:  
    def __init__(self, name, age, position, salary):  
        self.name = name  
        self.age = age  
        self.position = position  
        self.salary = salary  
  
    def increase_salary(self, percent):  
        self.salary += self.salary * (percent / 100)  
  
    def __str__(self):  
        return f'{self.name} is {self.position} and earns {self.salary}'  
  
    def __repr__(self):  
        return f"{type(self).__name__}({', '.join(f'{key}={val!r}' for key, val in vars(self).items())})"  
  
  
    @property  
    def salary(self, salary):  
        if salary < 10000:  
            raise ValueError("Salary too low")  
        self._salary = salary  
  
    @salary.setter  
    def salary(self):  
        return self._salary  
  
    @salary.deleter  
    def salary(self):  
        del self._salary  
  
    @property  
    def salart_gross(self):  
        return self.salary * 1.23
```
w py getter używa się do formatowania danych
setter -> data validation

jeśli napiszemy gettera dla czegoś, ale nie napiszemy do niego settera, to będzie to read only.

dziedziczenie służy głównie do specjalizacji klass
```python
class Employee:  
    def __init__(self, name, age, position, salary):  
        self.name = name  
        self.age = age  
        self.position = position  
        self.salary = salary  
  
    def increase_salary(self, percent):  
        self.salary += self.salary * (percent / 100)


class Tester(Employee):  
    def run_tests(self):  
        print(f"{self.name} is running tests")  
        print("all tests passed")



class Developer(Employee):  
    def increase_salary(self, percent, bonus=0):  
        self.salary += self.salary * (percent / 100) + bonus
```

overriding, gdy się nadpisuje metodę powinny mieć ten sam prototyp (ta sama ilość parametrówm, te same typingi

solid open close: raz napisana klasa nigdy nie powinna się zmienić

funkcjonalność multidziedziczenia, horyzontalne jest uważane za antypraktykę

wzorzec projektowy template - dziedziczenie getterów i setterów.

```python
class Empleyee:
	max_salary = 100 # to są atrybuty klasy
```
metody klasy to technicznie to samo co atrybuty, ale z jakimś callable


# Ask for forgiveness rather than permission
```python

x = 0  
if x != 0:  # ask for permission
    print(10 / x)                     
      
try:                        # ask for forgiveness  
    10 / x  
except ZeroDivisionError:  
    print("Division by zero")
``` 

super(). ... powoduje wywołanie tego co jest po kropce w klasie z której aktualna klasa dziedziczy

czym się rózni kompozycja od dziedziczenia:
dziedziczenie jest hierarchią, a kompozycja to przekazywanie jednych obiektów do innych obiektów

kompozycja jest lepsza o dziedziczenia, daje więcej możliwości, więcej elastyczności

vars(self) to \__dict__ obiektu

słabe referencje ; służą do śledzenia obiektu  .... 

jak działa lookup szukania pola obiektu w klasie:
- najpierw przeszukuje data object descriptory
- później sprawdza czy jest \__slots__
- później instance attr:
```python
if name in vars(self)
	return vars(self)[name]
```
- później nondata descriptor
- później class attr:
```python
if cls-attr is not None
	return cls-attr
```
- później sdzuka \_\_getattr__(self, name)
- później AttriburteError
![[Zrzut ekranu z 2025-01-19 10-05-11.png]]


Atrybuty klas mogą być  metodami lub polami klasy

data descriptior:
ma dunder get + dunder set lub delete

nondata descriptor:
- ma tylko get

jeśli używamy high level api (len(). repr(), str() itp.) to lookup szukania obiektu w klasie jest pomijany i idzie odrazu do.

#### WeakKeyDictionary:
tworzy słownik ze słabą referencją do obiektu. jeśłi obiekt zostanie zniszczony, to WKD zaczyna referować do None i nie utrzymuje obiektu przy życiu w pamięci![[Zrzut ekranu z 2025-01-19 10-29-02.png]]



wirtualne dziedziczenie:
issublass mówi że A jest podklasą B, ale w drzewie dziedziczenia A nie ma B. za to w A są metody z B

(żeby dało się iterować, po x to x musi spełniać protokół iteratora, czyli posiadać dunder iter i next. to właśnie wirtualne dziedziczenie)
wirtualne dziedziczenie, to inaczej gwarancja że spełnia się interfejs obiektu po którym się dziedziczy, ale nie dostaje się po tej klasie niczego.


metaklasy są klasami które tworzą klasy.
pozwalają zastosować metaprogramming - traktowanie kodu jako danych.


Indenpotentność. funkcja może być indenpotetntna, jeśli obsługuje dowolny typ danych bez błędów (???) czy za każdym razem tak samo


NotImplemented deleguje do dalszego przetwarzania,
NotImplementedError rzuca błąd i kończy zabawę