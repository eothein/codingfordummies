
## RSA

Belangrijk! DEZE CODE DIENT ENKEL TER ILLUSTRATIE!
NIET GEBRUIKEN VOOR DOELEINDEN WAARBIJ ECHTE VEILIGHEID VEREIST IS!


```python
## Berekent x, y en z zodat: ax + by = z en z = ggd(a,b)
def extended_euclid(a, b):
    r0 = a ; r1 = b
    s0 = 1 ; s1 = 0
    t0 = 0 ; t1 = 1
    while r1 != 0:
        q = r0 // r1
        (r0, r1) = (r1, r0 - q*r1)
        (s0, s1) = (s1, s0 - q*s1)
        (t0, t1) = (t1, t0 - q*t1)
    return (s0, t0, r0)
```


```python
## Berekent de inverse modulo n
def inverse_mod(x, n):
    (a, b, ggd) = extended_euclid(x, n)
    if ggd == 1:
        return a % n
    else:
        print("Error: inverse kan niet berekend worden!")
```


```python
## Berekent x^p mod m op een efficiënte manier.  Gebruikt de halveringsmethode.
## x : number to exponentiate
## p : exponent
## m : modulus
def pow_mod(x, p, m):
    if p == 0:
        return 1
    elif p == 1:
        return x % m
    else:
        half = p // 2
        pow_half = pow_mod(x, half, m)
        pow_half = (pow_half * pow_half) % m
        if p % 2 == 0:
            return pow_half
        else:
            return (pow_half * x) % m
```


```python
## Is een getal waarschijnlijk priem ?
## We gebruiken de Fermat test: voor een priemgetal p geldt dat a^(p-1) = 1 mod p
## Als men maw een getal a vindt (1 < a < p) waavoor a^(p-1) != 1 dan is p zeker NIET priem.
import random
def probably_prime_fermat(p, num_tries = 50):
    for i in range(num_tries):
        a = random.randint(2, p-1)
        if pow_mod(a, p - 1, p) != 1:
            return False # zeker geen priemgetal
    # Waarschijnlijk priem maar kan verkeerd zijn
    return True    

## Genereer een groot priemgetal
## Start bij een groot (oneven) random getal. Probeer de reeks start, start + 2, start + 4, ...
## tot men een priemgetal vindt. Dit zou normaalgezien tamelijk snel moeten gebeuren.
def generate_prime(lengte):
    start = random.randint(10**lengte, 100**lengte)
    if start % 2 == 0:
        start += 1
    # num = 1 ## aantal getallen geprobeerd
    while not probably_prime_fermat(start):
        # num += 1
        start += 2
    # print("Aantal getallen getest:", num)
    return start
```


```python
## Zet een boodschap om naar een getal.
## Boodschap mag enkel bestaan uit letters en spaties
## De boodschap wordt omgezet naar hoofdletters alvorens de omzetting
## naar een getal gebeurt.
def message_to_number(message):
    letters = " ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    number = ""
    for letter in message.upper():
        i = letters.index(letter)
        if (i < 10):
            number += "0" + str(i)
        else:
            number += str(i)
    return int(number)
## Omgekeerde bewerking van de vorige.
def number_to_message(number):
    letters = " ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    message = ""
    while number != 0:
        i = number % 100        
        message = letters[i] + message
        number //= 100
    return message
              
number_to_message(message_to_number("A PRIME"))    
```




    'A PRIME'




```python
probably_prime_fermat(98777056456123)
```




    False

    
