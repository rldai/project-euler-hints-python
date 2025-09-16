# The Problem

Project Euler often uses primes and it's convenient to have one place to store programs that can efficiently generate primes. That program can used over and over in multiple problems.

# Brute Force Solution
<details>
    <summary>
        How do I get started?
    </summary>
        Try making a for loop the calls a function that checks if the number is prime.
</details>

<details>
    <summary>
        Okay, but this is very slow...
    </summary>
        You may have something like this:<br>
  <code>upper_limit = 1000
primes = []
#
def is_prime(n):
    for factor in range(2, n):
        if n % factor == 0:
            return 0
    return 1
#
for i in range(2, upper_limit):
    if is_prime(i):
        primes.append(i)</code><br><br>
    Runtime when upper limit is 1000: 0.005 seconds <br>
    Runtime when upper limit is 10000: 0.2 seconds <br>
    Runtime when upper limit is 100000: 16 seconds <br>
  There are many ways to make this more efficient. <br><br>
  First, can you check if something is prime without checking every factor in range(2, n)? <br><br>
  Second, do you have to call the is_prime function for every i in range(2, upper_limit)? <br>
</details>

<details>
    <summary>
        I don't know the answers.
    </summary>
  First, you can use the list of primes instead of checking every factor in range(2, n). If a number is indivisible by every prime below it, it's prime. You also only have to check primes in range(2, sqrt(n)). If there were a prime factor larger than sqrt(n), then there would also be at least one prime factor smaller than sqrt(n). This means you could add a break statement or change the for loop to a while loop.<br><br>
  Second, you can also use the fact that 2 is the only even prime to check only the odd numbers. If a number is even, it can be skipped. 
</details>

<details>
    <summary>
        Final Solution:
    </summary>
  <code>upper_limit = 100
primes = []
#
def is_prime(n):
    square_root_of_n = n**0.5
    for prime in primes:
        if prime >= square_root_of_n:
            break
        if n % prime == 0:
            return 0
    return 1
#
for i in range(3, upper_limit,2):
    if is_prime(i):
        primes.append(i)
primes.insert(0, 2)</code><br><br>
        Runtime when upper limit is 1000: 0.0002 seconds <br>
    Runtime when upper limit is 10000: 0.004 seconds <br>
    Runtime when upper limit is 100000: 0.05 seconds <br>
    Runtime when upper limit is 1000000: 0.8 seconds <br>
</details>

# Nice Solution
<details>
    <summary>
        I feel like the brute force solution is still fundementally inefficient. I'm interested in another method.
    </summary>
        A nicer solution is a sieve. The Sieve of Eratosthenes an algorithm where you start with all composite numbers up to an upper limit. Then, you remove multiples of primes until only the primes are left. More elaboration will be in the next hint, but given this information, try coding the sieve yourself.
</details>

<details>
    <summary>
        I need more elaboration how to do that. 
    </summary>
        First, make a list of the composite numbers. You remove all multiples of 2 from the composite numbers. Then, you go to the next highest number that is not eliminated. That's 3. Its multiples are eliminated. The next highest number is 4, but that was eliminated when all the multiples of 2 were eliminated. So, the next number is 5. This continues for all numbers less than the upper limit.<br><br>
    Consider modifying the sieve with a time-saving measure that was included in the brute force solution.
</details>

<details>
    <summary>
        So what is that in code form? 
    </summary><code>upper_limit= 1000
primes_set = {2}
#
for i in range(3, upper_limit, 2):
    primes_set.add(i)
#
factor = 3
square_root_of_upper_limit = upper_limit**0.5
while factor <= square_root_of_upper_limit:
    multiples_of_factor = upper_limit // factor
    for i in range(3, multiples_of_factor + 1, 2):
        primes_set.discard(factor * i)
    factor += 2
#
primes = list(primes_set)</code><br><br>
    Runtime when upper limit is 1000: 0.0001 seconds <br>
    Runtime when upper limit is 10000: 0.002 seconds <br>
    Runtime when upper limit is 100000: 0.02 seconds <br>
    Runtime when upper limit is 1000000: 0.2 seconds <br>
    Runtime when upper limit is 10000000: 3 seconds <br>
</details>

<details>
    <summary>
        But can you make it better?
    </summary>
    You can make the program faster by excluding multiples of 3.
</details>

<details>
    <summary>
        Final Solution (The Author):
    </summary>
    <code>upper_limit= 10000000
primes_set = {2, 3}
#
for i in range(5, upper_limit, 2):
    if i % 3 != 0:
        primes_set.add(i)
#
factor = 5
square_root_of_upper_limit = upper_limit**0.5
while factor <= square_root_of_upper_limit:
    multiples_of_factor = upper_limit // factor
    for i in range(3, multiples_of_factor + 1, 2):
        if i % 3 != 0:
            primes_set.discard(factor * i)
    factor += 2
    if factor % 3 == 0:
        factor = factor + 2
#
primes = list(primes_set)</code><br><br>
        Runtime when upper limit is 1000: 0.00015 seconds <br>
    Runtime when upper limit is 10000: 0.0015 seconds <br>
    Runtime when upper limit is 100000: 0.015 seconds <br>
    Runtime when upper limit is 1000000: 0.16 seconds <br>
    Runtime when upper limit is 10000000: 2 seconds <br><br>
    (AN: This might be extended for multiples of 5, but there are diminishing returns. It seems like excluding multiples of 3 makes the program runtime 3/2 = 1.5 times faster. Exclusding multples of 5 maybe make the program runtime 5/4 = 1.25 times faster, but at that point, the program is likely fast enough.) <br><br>
    (AN: There are other ways to optomize the sieve, which can be found on <cite
      ><a href="https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes"
        >Wikipedia</a
      ></cite
    >. Those are outside the scope of this project.)
</details>
