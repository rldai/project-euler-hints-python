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
  <code>upper_limit = 100
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
  There are many ways to make this more efficient. <br>
  First, can you check if something is prime without checking every factor in range(2, n)? <br>
  Second, do we have to call the is_prime function for every i in range(2, upper_limit)? <br>
</details>

<details>
    <summary>
        I don't know the answers.
    </summary>
  First, we can use the list of primes instead of checking every factor in range(2, n). If a number is indivisible by every prime below it, it's prime. We also only have to check primes in range(2, sqrt(n)). If there were a prime factor larger than sqrt(n), then there would also be at least one prime factor smaller than sqrt(n). <br>
  Second, we can also use the fact that 2 is the only even prime to check only the odd numbers. If a number is even, it can be skipped. 
</details>
