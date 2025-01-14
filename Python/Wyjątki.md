
## kiedy stosować:
kiedy program nie może dalej działać w danym przypadku

### lista wyjątków
[https://docs.python.org/3/library/exceptions.html#exception-hierarchy](https://docs.python.org/3/library/exceptions.html#exception-hierarchy)


w py obsługa wyjątków jest 3 poziomowa
1. try except
2. assert
3. context manager


### context manager
można go zapisać za pomocą klasy i spełnienu protokołu, albo z dekoratorem
aby użyć with Klasa() as kl
Klasa musi mieć dunder enter i exit


### transakcja
zestaw operacji, które muszą być wykonane wszystkie albo żadna