1- take two large primes
`p` and `q`

2- `n = p.q`

## Euler totient function
`phi(n)` : number of numbers  `<n` coprime to n
x and n are coprime, means their greatest common denominator is 1: gcd(n,x)= 1

>for prime numbers, **`phi(x)= x-1`** cause they're prime divisible just by one so the gcd(x,y) with x<n is always 1

p and q are prime not n, but:
3- `phi(n) = phi(p.q) = phi(q).phi(p)= (q-1).(p-1)`
## Public key
`e => 2 < e <phi(n) and gcd(e, phi(n))=1`
## Private key
d as:
`e.d = 1 mod phi(n)`
=>`(e.d)%phi(n) = 1`  using extended euclidean algorithm or brute force d for d in range(2,phi(n))

## cipher
m: message
`c = m**e mod n`
## decrypt
`m = c**d mod n`
## siignature
`s = m**d mod n`
## check signature
`m = s**e mod n`