# Handling Missing Data in Pandas: A Complete Guide

## **What is Missing Data?**
**Missing data** happens when some information isn't available in your dataset - like empty cells in Excel or blank entries in a database. In the weather example, some days have no temperature or event recorded.

## **Key Concepts Explained Simply:**

### **1. Understanding NaN (Not a Number)**
- **What it is**: `NaN` is pandas' way of saying "this value is missing"
- **How to spot it**: Empty cells, `null`, `NA`, or `None` values
- **Example**: Your weather data shows blank spots for January 2nd and 3rd

### **2. Methods to Handle Missing Data:**

#### **A. fillna() - Replace Missing Values**
**What it does**: Fills empty spots with a value you choose

```python
# Fill all missing values with 0
df.fillna(0)

# Fill different columns with different values
df.fillna({
    'temperature': 0,
    'wind_speed': 0,
    'event': 'no event'
})
```

**Types of fillna():**
- **Forward Fill**: Copy from the previous day
  ```python
  df.fillna(method='ffill')  # Forward fill
  ```
  *Example*: If Monday's temperature was 32°F and Tuesday is missing, Tuesday becomes 32°F

- **Backward Fill**: Copy from the next day
  ```python
  df.fillna(method='bfill')  # Backward fill
  ```
  *Example*: If Wednesday's temperature was 28°F and Tuesday is missing, Tuesday becomes 28°F

#### **B. dropna() - Remove Missing Values**
**What it does**: Deletes rows or columns with missing data

```python
# Drop rows with ANY missing values (default)
df.dropna()

# Drop rows where ALL values are missing
df.dropna(how='all')

# Keep rows with at least 2 valid values
df.dropna(thresh=2)
```

**When to use**: When missing data is minimal and won't affect your analysis much

#### **C. interpolate() - Smart Guessing**
**What it does**: Calculates missing values based on existing data

```python
# Linear interpolation (straight line between points)
df.interpolate()

# Time-based interpolation (considers dates/times)
df.interpolate(method='time')
```

**Example**: If Monday = 32°F and Friday = 28°F, interpolate() might guess Wednesday = 30°F

### **3. Important Parameters:**

#### **Axis (Rows vs Columns)**
- **axis=0** (default): Work vertically (down the rows)
- **axis=1**: Work horizontally (across columns)

#### **Limit - Control How Many to Fill**
```python
# Fill only 1 missing value after each valid value
df.fillna(method='ffill', limit=1)
```
*Use case*: Prevent copying too far forward/backward

### **4. Dealing with Missing Dates:**

```python
# Create complete date range
full_dates = pd.date_range(start='2023-01-01', end='2023-01-11')

# Reindex to include missing dates
df = df.reindex(full_dates)
```

**What happens**: Adds January 2nd, 3rd (or any missing dates) with NaN values

## **When to Use Each Method:**

| Situation | Best Method | Why |
|-----------|-------------|-----|
| **Missing weather data** | `interpolate(method='time')` | Weather changes gradually over time |
| **Missing event/category** | `fillna()` with 'unknown' | Categories don't interpolate well |
| **Very few missing values** | `dropna()` | Simple, won't lose much data |
| **Predictable patterns** | `fillna(method='ffill')` | Good for repeated measurements |
| **Before/after values known** | `fillna(method='bfill')` | When future values exist |

## **Practical Tips:**

1. **Always check first**: Use `df.isna().sum()` to see how much data is missing
2. **Think about meaning**: Is 0°F reasonable for missing temperature? Maybe use interpolation instead
3. **Document your choices**: Note why you chose a particular method
4. **Try multiple approaches**: Compare results to see which makes most sense
5. **Consider the impact**: Will your analysis change dramatically based on how you fill missing values?

## **Real-World Example:**

Imagine tracking daily coffee sales:
- Monday: 100 cups ✓
- Tuesday: ? cups (missing)
- Wednesday: 120 cups ✓
- Thursday: ? cups (missing)
- Friday: 140 cups ✓

**Your options:**
1. **fillna(0)**: Tuesday = 0, Thursday = 0 (unrealistic - you never sell 0 coffee)
2. **ffill**: Tuesday = 100, Thursday = 120 (copy from previous day)
3. **interpolate**: Tuesday = 110, Thursday = 130 (average of neighbors)
4. **dropna()**: Just analyze Monday, Wednesday, Friday

**Best choice**: Probably `interpolate()` since sales usually follow patterns!

## **Key Takeaways:**
- **Missing data is common** - don't panic!
- **No one-size-fits-all** - choose method based on your data type
- **Time matters** - Use time-aware methods for dates/times
- **Document everything** - Note how you handled missing values
- **Check impact** - Make sure your method doesn't distort results

**Remember**: The goal is to make your data complete enough for analysis while keeping it as realistic as possible. Start with the simplest method that makes sense for your data!