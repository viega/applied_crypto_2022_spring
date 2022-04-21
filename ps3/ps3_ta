#!/usr/bin/env python3
import json
import math
import sys
import typing
from dataclasses import dataclass, field


def is_prime_naive(x: int) -> bool:
    """
    Pretty naive algorithm which only optimizes %2 as well as only checks up to
    sqrt of number

    >>> is_prime_naive(3)
    True
    >>> is_prime_naive(4)
    False
    >>> is_prime_naive(9)
    False
    >>> is_prime_naive(19)
    True
    """
    assert x > 0
    if x == 1:
        return False
    elif x in (2, 3):
        return True
    elif x % 2 == 0:
        return False
    for i in range(3, max(3, math.ceil(math.sqrt(x))) + 1, 2):
        if x % i == 0:
            return False
    return True


def gcd(x: int, y: int) -> int:
    """
    uses eucledian algorithm
    https://en.wikipedia.org/wiki/Euclidean_algorithm

    >>> gcd(24, 30)
    6
    >>> gcd(12, 45)
    3
    >>> gcd(270, 192)
    6
    """
    while y:
        x, y = y, x % y
    return x


def gcd_extended(a: int, b: int) -> typing.Tuple[int, int, int]:
    """
    uses eucledian extended algorithm
    https://en.wikipedia.org/wiki/Extended_Euclidean_algorithm

    >>> gcd_extended(192, 270)
    (6, -7, 5)
    """
    c, d = a, b
    uc, vc, ud, vd = 1, 0, 0, 1
    while c:
        q = d // c
        c, d = d - q * c, c
        uc, vc, ud, vd = ud - q * uc, vd - q * vc, uc, vc
    assert d == a * ud + b * vd
    return d, ud, vd


def lcm(x: int, y: int) -> int:
    """
    uses gcd to make it faster without loops
    https://en.wikipedia.org/wiki/Least_common_multiple

    >>> lcm(6, 10)
    30
    """
    return (x * y) // gcd(x, y)


def multicative_inverse(i: int, p: int) -> int:
    """
    >>> multicative_inverse(10, 17)
    12
    >>> multicative_inverse(5, 17)
    7
    >>> multicative_inverse(7, 30)
    13
    """
    assert i < p
    naive = _multicative_inverse_naive(i, p)
    extended = _multicative_inverse_extended_euclid(i, p)
    assert naive == extended
    return extended


def _multicative_inverse_extended_euclid(i: int, p: int) -> int:
    d, r, s = gcd_extended(i, p)
    assert d == 1
    assert i * r + p * s == 1
    return r % p


def _multicative_inverse_naive(i: int, p: int) -> int:
    for j in range(1, p):
        if (i * j) % p == 1:
            return j
    raise ValueError(
        f"{i} does not have multicative inverse for multicative group mod {p}"
    )


def choose_e(l: int) -> int:
    """
    very naive algorithm

    >>> choose_e(30)
    7
    """
    for i in range(2, l):
        if gcd(i, l) == 1:
            return i
    raise ValueError(f"did not find valid e for {l}")


@dataclass
class RSA:
    p: int
    q: int
    n: int = field(init=False)
    l: int = field(init=False)
    phi: int = field(init=False)
    order_l: bool = field(default=True, repr=False)
    e: int = field(init=False)
    d: int = field(init=False)

    def __hash__(self):
        return hash(self.p * self.q)

    def __post_init__(self):
        assert is_prime_naive(self.p)
        assert is_prime_naive(self.q)
        self.derive_components()

    def derive_components(self):
        self.n = self.p * self.q
        self.phi = (self.p - 1) * (self.q - 1)
        self.l = lcm(self.p - 1, self.q - 1)
        order = self.l if self.order_l else self.phi
        self.e = choose_e(order)
        self.d = multicative_inverse(self.e, order)

    def encrypt(self, x):
        y = (x ** self.e) % self.n
        assert x == (y ** self.d) % self.n, (self, x)
        return y

    def decrypt(self, y):
        x = (y ** self.d) % self.n
        assert y == (x ** self.e) % self.n, (self, y)
        return x


@dataclass
class Problem1:
    nums: typing.List[int]


def problem1(data: Problem1):
    return [is_prime_naive(i) for i in data.nums]


Problem2 = RSA


def problem2(data: Problem2):
    return data.e


Problem3 = RSA


def problem3(data: Problem3):
    return data.d


@dataclass
class Problem4:
    x: int
    e: int
    n: int


def problem4(data: Problem4):
    return data.x ** data.e % data.n


@dataclass
class Problem5:
    y: int
    p: int
    q: int


def problem5(data: Problem5):
    rsa = RSA(p=data.p, q=data.q)
    return rsa.decrypt(data.y)


if __name__ == "__main__":
    data = json.loads(sys.stdin.read())
    solutions = {
        k: globals()[k.replace(" ", "")](globals()[k.replace(" ", "").title()](**v))
        for k, v in data.items()
    }
    print(json.dumps(solutions, indent=4))
