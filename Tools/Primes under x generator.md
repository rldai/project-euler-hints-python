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
    (AN: There will be a graph below comparing the solutions!)
  There are many ways to make this more efficient. <br>
  First, can you check if something is prime without checking every factor in range(2, n)? <br>
  Second, do you have to call the is_prime function for every i in range(2, upper_limit)? <br>
</details>

<details>
    <summary>
        I don't know the answers.
    </summary>
  First, you can use the list of primes instead of checking every factor in range(2, n). If a number is indivisible by every prime below it, it's prime. You also only have to check primes in range(2, sqrt(n)). If there were a prime factor larger than sqrt(n), then there would also be at least one prime factor smaller than sqrt(n). This means you could add a break statement or change the for loop to a while loop.<br>
  Second, you can also use the fact that 2 is the only even prime to check only the odd numbers. If a number is even, it can be skipped. 
</details>

<details>
    <summary>
        Final Solution (The Author):
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
        I feel like the brute force solution is still fundementally inefficient. I/m interested in another method.
    </summary>
        A nicer solution is a sieve. The Sieve of Eratosthenes an algorithm where you start with all composite numbers up to an upper limit. Then, you remove multiples of primes until only the primes are left. More elaboration will be in the next hint, but given this information, try coding the sieve yourself.
</details>

<details>
    <summary>
        I need more elaboration on what that is. 
    </summary>
        First, you remove all multiples of 2 from the composite numbers. Then, you go to the next highest number that is not eliminated. That's 3. Its multiples are eliminated. The next highest number is 4, but that was eliminated when all the multiples of 2 were eliminated. So, the next number is 5. This continues for all numbers less than the upper limit.
</details>

