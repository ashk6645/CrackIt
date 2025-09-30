# Simple & Compound Interest

>Status: 🟢 Complete — comprehensive guide with formulas, comparisons, and practice problems.

## 🚀 Quick Overview

Simple and Compound Interest problems are fundamental in quantitative aptitude, testing your understanding of financial mathematics. These problems appear frequently in banking exams, MBA entrance tests, and placement assessments. Master these concepts to handle investment, loan, and growth-related questions.

## 📚 Core Concepts

### Simple Interest (SI)
Interest calculated only on the principal amount throughout the investment period.

### Compound Interest (CI)  
Interest calculated on principal plus accumulated interest from previous periods.

### Key Terms
- **Principal (P)**: Initial amount invested/borrowed
- **Rate (R)**: Annual interest rate (%)
- **Time (T)**: Duration of investment/loan (years)
- **Amount (A)**: Principal + Interest
- **Simple Interest**: Interest earned on principal only
- **Compound Interest**: Interest earned on principal + accumulated interest

## 🧮 Essential Formulas

### Simple Interest Formulas
| Concept | Formula |
|---------|---------|
| Simple Interest | SI = (P × R × T) / 100 |
| Amount | A = P + SI = P(1 + RT/100) |
| Principal | P = (100 × SI) / (R × T) |
| Rate | R = (100 × SI) / (P × T) |
| Time | T = (100 × SI) / (P × R) |

### Compound Interest Formulas
| Concept | Formula |
|---------|---------|
| Amount (Annual) | A = P(1 + R/100)^T |
| Amount (n times/year) | A = P(1 + R/(100n))^(nT) |
| Compound Interest | CI = A - P |
| Present Value | PV = A / (1 + R/100)^T |

### Special Cases
| Compounding | Formula |
|-------------|---------|
| Half-yearly | A = P(1 + R/200)^(2T) |
| Quarterly | A = P(1 + R/400)^(4T) |
| Monthly | A = P(1 + R/1200)^(12T) |
| Continuous | A = Pe^(RT/100) |

## 🔄 SI vs CI Comparison

### Difference Between CI and SI
- **For 1 year**: CI = SI (always)
- **For 2 years**: CI - SI = P(R/100)²
- **For 3 years**: CI - SI = P(R/100)² × (300 + R)/100

### When CI > SI
- CI is always greater than SI for periods > 1 year
- Difference increases with time and rate

## 🧑‍💻 Solved Examples

### Example 1: Basic Simple Interest
**Q**: Find the simple interest on Rs. 8000 at 5% per annum for 3 years.

**Solution**:
- P = Rs. 8000, R = 5%, T = 3 years
- SI = (P × R × T) / 100 = (8000 × 5 × 3) / 100 = Rs. 1200

### Example 2: Basic Compound Interest
**Q**: Find the compound interest on Rs. 5000 at 10% per annum for 2 years.

**Solution**:
- P = Rs. 5000, R = 10%, T = 2 years
- A = P(1 + R/100)^T = 5000(1 + 10/100)² = 5000(1.1)² = 5000 × 1.21 = Rs. 6050
- CI = A - P = 6050 - 5000 = Rs. 1050

### Example 3: Difference Between CI and SI
**Q**: Find the difference between CI and SI on Rs. 4000 at 10% per annum for 2 years.

**Solution**:
Method 1 (Direct calculation):
- SI = (4000 × 10 × 2) / 100 = Rs. 800
- CI = 4000(1.1)² - 4000 = 4840 - 4000 = Rs. 840
- Difference = 840 - 800 = Rs. 40

Method 2 (Formula):
- Difference = P(R/100)² = 4000 × (10/100)² = 4000 × 0.01 = Rs. 40

### Example 4: Half-yearly Compounding
**Q**: Find the amount when Rs. 10000 is invested at 12% per annum compounded half-yearly for 1.5 years.

**Solution**:
- P = Rs. 10000, R = 12%, T = 1.5 years
- For half-yearly: R = 12/2 = 6%, T = 1.5 × 2 = 3 periods
- A = P(1 + R/100)^T = 10000(1 + 6/100)³ = 10000(1.06)³
- A = 10000 × 1.191016 = Rs. 11910.16

### Example 5: Finding Principal
**Q**: What principal will amount to Rs. 8820 in 2 years at 5% compound interest per annum?

**Solution**:
- A = Rs. 8820, R = 5%, T = 2 years
- A = P(1 + R/100)^T
- 8820 = P(1.05)²
- 8820 = P × 1.1025
- P = 8820/1.1025 = Rs. 8000

### Example 6: Population Growth
**Q**: The population of a town increases by 10% annually. If the current population is 50,000, what will be the population after 3 years?

**Solution**:
- Using CI formula: A = P(1 + R/100)^T
- Population after 3 years = 50000(1 + 10/100)³
- = 50000(1.1)³ = 50000 × 1.331 = 66,550

### Example 7: Variable Rates
**Q**: Rs. 1000 is invested at 10% for the first year, 12% for the second year, and 15% for the third year, compounded annually. Find the amount.

**Solution**:
- After 1st year: A₁ = 1000(1.10) = Rs. 1100
- After 2nd year: A₂ = 1100(1.12) = Rs. 1232  
- After 3rd year: A₃ = 1232(1.15) = Rs. 1416.80

### Example 8: Installments
**Q**: A person borrows Rs. 10000 at 20% CI per annum. He repays Rs. 4000 at the end of first year and Rs. 5000 at the end of second year. How much should he pay at the end of third year to clear the debt?

**Solution**:
- Amount after 1 year = 10000(1.20) = Rs. 12000
- After paying Rs. 4000: Balance = 12000 - 4000 = Rs. 8000
- Amount after 2 years = 8000(1.20) = Rs. 9600
- After paying Rs. 5000: Balance = 9600 - 5000 = Rs. 4600  
- Amount after 3 years = 4600(1.20) = Rs. 5520

## 🔥 Advanced Topics

### 1. Effective Annual Rate
When compounded n times per year:
**Effective Rate = (1 + r/n)ⁿ - 1**

### 2. Present Value & Future Value
- **PV = FV / (1 + r)ⁿ**
- **FV = PV × (1 + r)ⁿ**

### 3. Doubling Time
Time to double money at r% CI:
**T ≈ 72/r** (Rule of 72)

### 4. Depreciation
Using CI formula with negative rate:
**A = P(1 - R/100)ᵀ**

## � Practice Drill (15 Questions)

### Basic Level (2-3 minutes each)
1. SI on Rs. 2000 at 8% for 5 years?
2. CI on Rs. 1000 at 10% for 2 years?
3. Time to earn Rs. 500 SI on Rs. 2500 at 5%?

### Intermediate Level (4-5 minutes each)
4. Difference between CI and SI on Rs. 6000 at 15% for 2 years?
5. Amount when Rs. 8000 compounded quarterly at 16% for 9 months?
6. Population grows 5% annually. Current: 20000. After 3 years?

### Advanced Level (6-8 minutes each)
7. What principal amounts to Rs. 13310 in 3 years at 10% CI?
8. A sum doubles in 5 years at CI. In how many years will it become 8 times?
9. Rs. 10000 borrowed at 12% CI. Repaid Rs. 3000 after 1 year, Rs. 4000 after 2 years. Balance after 3 years?

## 📚 Additional Resources

- [Compound Interest Calculator](https://www.calculator.net/compound-interest-calculator.html)
- [Financial Mathematics (Khan Academy)](https://www.khanacademy.org/economics-finance-domain)
- [Banking & Finance Problems](https://www.indiabix.com/aptitude/simple-interest/)

## 🎯 Answer Key

1. Rs. 800  2. Rs. 210  3. 4 years  4. Rs. 135  5. Rs. 8955.05  6. 23,152  7. Rs. 10000  8. 15 years  9. Rs. 5260.80

---

>**Last Updated**: September 2025 | **Contributor**: CrackIt Team
