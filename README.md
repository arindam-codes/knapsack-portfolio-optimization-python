# Greedy Stock Selection — 0/1 Knapsack Problem in Python
> Compare three greedy strategies for portfolio optimization using Python. Which one picks the best stocks under a $1000 budget?

A small modeling exercise inspired by **MIT 6.100B (Lecture 1)** 

---

## Problem Statement

I have a **fixed budget**(total weight capacity) and i have to choose the best possible **stocks**(elements) to get the best possible output

Each stock has **Price (weight / cost)** and **Expected return (value)**

and i can only buy whole shares (0/1 decision) which is the classic **0/1 Knapsack problem**.

I have to solve this using **Greedy Algorithm** in **Python**.

---
## Code Snippet

### I modelled each stocks using the name of the stock company, **price** and **expected return**
```
class StockTicker():
    
    def __init__(self, name, price, expectedReturn):
        self.name = name
        self.price = price
        self.expectedReturn = expectedReturn
        
    def get_name(self):
        return self.name
        
    def get_price(self):
        return self.price
    
    def get_expectedReturn(self):
        return self.expectedReturn

```
### The main **Greedy** Engine
```
def greedy(stocks, budget, keyFunction):
    
    stockItems = sorted(stocks, key = keyFunction, reverse=True)
    profitableStocks = []
    investment = 0
    
    for stock in stockItems:
        if stock.get_price() + investment <= budget:
            profitableStocks.append(stock)
            investment += stock.get_price()
            
    return profitableStocks

```

---

## 3 Greedy Strategies **Highest Expected Return First** | **Lowest Cost First** | **Highest Return per Dollar (Value/Weight Ratio)**

1. **Highest Expected Return First**
```
# returns by expected return
    r_probablestocks = greedy(stocks, budget, lambda stock: stock.get_expectedReturn())
    stockPrinter(r_probablestocks)
```
2. **Lowest Cost First**
```
# returns by price (cost)
    c_probablestocks = greedy(stocks, budget, lambda stock: 1 / stock.get_price())
    stockPrinter(c_probablestocks)
```
3. **Highest Return per Dollar (Value/Weight Ratio)**
```
 # returns by return per dollar 
    rpd_probablestocks = greedy(stocks, budget, lambda stock: stock.get_expectedReturn() / stock.get_price())
    stockPrinter(rpd_probablestocks)
    
```
---

## Dataset

| Stock | Price ($) | Expected Return ($) |
| ----- | --------- | ------------------- |
| AAPL  | 175       | 15                  |
| GOOG  | 140       | 12                  |
| MSFT  | 330       | 28                  |
| AMZN  | 145       | 11                  |
| TSLA  | 200       | 18                  |
| META  | 320       | 25                  |
| NFLX  | 500       | 40                  |
| NVDA  | 800       | 70                  |

---

## Results (Budget: $1000)

3 strategies on this dataset:

### 1. Highest Expected Return First
- **Selected:** NVDA ($800, returns $70) + TSLA ($200, returns $18)
- **Total return:** $88
- **Budget used:** $1000

### 2. Lowest Cost First
- **Selected:** GOOG ($140) + AMZN ($145) + AAPL ($175) + TSLA ($200) + META ($320)
- **Total return:** $81
- **Budget used:** $980 ($20 leftover)

### 3. Highest Return per Dollar
- **Selected:** TSLA ($200) + NVDA ($800)
- **Total return:** $88
- **Budget used:** $1000

### Key Takeaway
Highest Expected Return and Highest Return per Dollar tied at **$88**. Lowest Cost First performed worst at **$81**, even though it bought more stocks.

---

## What I Larned
* Greedy does not provides everytime the best guaranteed solutions
* I modelled the Stocks using OOP 
* Helped me to enhance my Algorithmic thinking
---

I would love to apply this concept in:

* Optimization
* Quantitative finance modeling
* Resource allocation systems

---

## Learning Context

Built while studying:

* MIT 6.100B Lecture 1
* Greedy algorithms
* 0/1 knapsack foundations

---
📁 **Full code available** — check the **[greedy.py](https://github.com/arindam-codes/knapsack-portfolio-optimization-python/blob/main/greedy.py)** file in this repo.
