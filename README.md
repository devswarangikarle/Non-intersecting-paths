# Non-intersecting-paths

In a vibrant kingdom, a clever architect named "Elysia" was given 2*N enchanted stones arranged in a line. Her task was to design N non-intersecting bridges connecting these stones in pairs, creating a beautiful network. Elysia wanted to know how many unique ways she could construct these bridges without any of them overlapping. She needed to calculate this number while keeping her results within the magical limit of 109 + 7, a safeguard against overwhelming magic.
Can you assist Elysia in determining the total number of distinct arrangements to build the bridges between the enchanted stones?

This problem is related to the Catalan number sequence, which counts the number of ways to pair up items without crossing or intersecting connections. Specifically, the N-th Catalan number gives the number of non-intersecting ways to connect 2𝑁 items.
The formula for the N-th Catalan number is:

C(N)= (2N)!/(N+1)!.N!
Since the problem asks for the result modulo 10^9+7,  we will compute 𝐶(𝑁) efficiently using modular arithmetic.

Approach:
Precomputations:
-Use modular arithmetic to compute factorials up to 2N modulo 10^9+7.
-Precompute modular inverses of these factorials using Fermat's Little Theorem.

Catalan Calculation:
Compute 𝐶(𝑁) using the formula:
𝐶(𝑁)= fact[2N]/ fact[N]⋅fact[N+1] * mod(10^9 +7)

Simplify this using modular inverses:
C(N)= fact[2N]*inv_fact[N]*inv_fact[N+1] mod(10^9 +7)

Output:
For the input 𝑁, output 𝐶(𝑁).

MOD = 10**9 + 7

def modular_exponentiation(base, exp, mod):
    result = 1
    while exp > 0:
        if exp % 2 == 1:
            result = (result * base) % mod
        base = (base * base) % mod
        exp //= 2
    return result

def precompute_factorials(max_n, mod):
    fact = [1] * (2 * max_n + 1)
    for i in range(2, 2 * max_n + 1):
        fact[i] = (fact[i - 1] * i) % mod
    
    inv_fact = [1] * (2 * max_n + 1)
    inv_fact[2 * max_n] = modular_exponentiation(fact[2 * max_n], mod - 2, mod)
    for i in range(2 * max_n - 1, 0, -1):
        inv_fact[i] = (inv_fact[i + 1] * (i + 1)) % mod
    
    return fact, inv_fact

def catalan_number(n, fact, inv_fact, mod):
    return (fact[2 * n] * inv_fact[n] % mod * inv_fact[n + 1]) % mod

if __name__ == "__main__":
    import sys
    input = sys.stdin.read
    N = int(input().strip())
    
    # Precompute factorials and modular inverses
    fact, inv_fact = precompute_factorials(N, MOD)
    
    # Calculate the Nth Catalan number
    result = catalan_number(N, fact, inv_fact, MOD)
    
    print(result)





​
