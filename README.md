# Exercise 2



## Objectives :full_moon_with_face: 
- Learn how program effectively using if/else and iterations statements;
- Become familiar with using data frame objects and other data structures;
- Use some matrix calculus in R.



## Content :rocket: 



### Problem 1: Are you a power?
Write a program that prints the numbers from 1 to 100, but with the specific requirement:

- if the number is a full square of another number $a$, print `a^2`;
- if the number is a full cube of another number $b$, print `b^3`;
- if the number is a full square of another number $a$ **and** a full cube of another number $b$, print `a^2, b^3`.

An example of the output would be:

```{r}
"1^2, 1^3" "2" "3" "2^2" "5" "6" "7" "2^3" "3^2" "10" "11" "12" "13" "14" "15" "4^2" "17" "18", ...
```


### Problem 1: solution

Below is a possible solution for "Are you a power?". The `%in%` returns `TRUE` if the element belongs to the set, or `FALSE` otherwise.


```{r}
numbers <- character(100)
squares <- (1:10)^2
cubes <- (1:4)^3
for (k in 1 : length(numbers)) {
  if (k %in% squares && k %in% cubes) {
    numbers[k] <- paste0(which(squares == k), "^2, ", which(cubes == k), "^3")
  } else if (k %in% squares) {
    numbers[k] <- paste0(which(squares == k), "^2")
  } else if (k %in% cubes) {
    numbers[k] <- paste0(which(cubes == k), "^3")
  } else {
    numbers[k] <- k
  }
}
numbers
```


### Problem 2: Stock price and European call option

Let a stock price at time $t$ be $S(t) \equiv S_t$. Assume that $S(t)$ follows a Geometric Brownian Motion (GBM) given by:

$$\mathrm{d}S_t = r\,S_t  + \sigma \, S_t \, \mathrm{d}W_t, \quad 0 < t < 1,$$

where $S(0) = 1$, $r$ is a percentage drift, $\sigma$ is a percentage volatility, and $W_t$ is a Brownian motion.

To simulate from this continuous time series model one can use the Euler-Maruyama discretisation method with a constant temporal step $\tau$:

$$S_{m+1} = S_m + r\,S_m\,\tau + \sigma\,S_m\,\Delta W_m, \quad S_0 = 1,$$

where $\Delta W_m$ are i.i.d. centered normally distributed random variables with variance $\tau$, $m = 0, 1, 2, \ldots, N_t - 1$, $N_t = \text{ceiling}(1/\tau) + 1$ is the number of temporal steps at which the values $S_m$ are calculated (including $0$ and the first temporal step that exceeds $1$, if necessary).

A European call option with the strike price $K$ can be expressed as

$$Y = \exp(-r) \cdot \max\\{0; S(1) - K\\}.$$

The value of $Y$ can be approximated using a Monte-Carlo method: consider $N$ Euler-Maruyama simulations of the paths $S(t)$; for each simulation $n = 1, 2, \ldots, N$ calculate $Y_{n}$ using the above mentioned formula; eventually, approximate the value of $Y$ by taking the mean $\bar{Y}$.

For the following parameters

|Parameter|Value|
|---|---|
|$r$|0.05|
|$\sigma$|0.2|
|$\tau$|0.001|
|$K$|1|
|$N$|500|

- **(a)** Simulate $N$ paths of the stock price $S(t)$ using the Euler-Maruyama method. Plot some of these paths and comment on them. Do you think this model reflect what you could observe on the stock market? What features seem striking?

- **(b)** Calculate $N$ European call option prices $Y_n$, $n = 1, 2, \ldots, N$ and plot the average option price `Y_bar = mean(Y_n)`. Is it what you were expecting?

- **\(c)** Find and plot with a green color the path $S(t)$ versus the time $t$, which led to the highest value of the option price, i.e. the path $S(t)$ corresponding to $\max(Y_n)$;

- **(d)** On the same graph plot the path $S(t)$, which led to the lowest value of the option price, i.e. the path $S(t)$ corresponding to $\min(Y_n)$;

- **(e)** Finally, on the same graph plot the path $S(t)$, which led to the value $Y_k$ that is the closest to the estimate $\bar{Y}$, i.e. the path $S(t)$ corresponding to $\min(|Y_n - \bar{Y}|)$.

### Problem 3: portfolio construction
Suppose that you are working in an investment firm company as a quantitative analyst. Your boss gives you the task of creating a portfolio for one of your client. The client wants to find the portfolio with the smallest variance that satisfies the following constraints:

- Invest exactly $1,000,000.
- Invest in exactly two stocks of the S&P500 index.

Therefore, your boss requires that you compute all possible portfolios that satisfy the client's constraints, represent them graphically as (for example) in the graph below and find the weight of the best (i.e. minimum variance) portfolio.

<img src="hw2_Pr4_portfolio.png" alt="map" width="600px"/>

Using the dataset `stocks.rds`, fulfill the task. Hint: you may want to use the formulas and code [here](https://smac-group.github.io/ds/section-data.html#section-example-portfolio-optimization) for constructing the portfolios.

### Problem 4: solving a maze
Follow instructions and exercise 4 provided [here](https://intro-to-ds.netlify.app/chapter2).
