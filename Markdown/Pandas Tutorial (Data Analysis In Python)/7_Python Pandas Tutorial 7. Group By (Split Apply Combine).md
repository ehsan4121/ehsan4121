# **Complete Guide to Pandas Group By (Split-Apply-Combine)**

## **📌 What is Group By?**
Group By is like **organizing toys into different boxes**:
- Imagine you have mixed toys (cars, dolls, blocks)
- You put all cars in one box, dolls in another, blocks in another
- Then you can count how many are in each box or find the biggest toy in each box

**In pandas**: You group similar rows together (like all New York data together, all Mumbai data together) and then perform calculations on each group.

## **🔑 Key Concepts & Keywords**

### **1. Grouping (Splitting)**
- **Purpose**: Divide your data into groups based on a column value
- **Syntax**: `df.groupby('column_name')`
- **Example**: 
```python
# Group students by their class
students.groupby('class')
# Group sales data by month
sales.groupby('month')
```

### **2. GroupBy Object**
- **What it is**: Not a DataFrame, but a special object containing groups
- **Visualize**: Like having multiple mini-DataFrames in a dictionary
```python
# Internal structure looks like:
{
    'New York': [row1, row2, row3],
    'Mumbai':   [row4, row5],
    'Paris':    [row6, row7]
}
```

### **3. Split-Apply-Combine Process**
This is the **core philosophy** behind Group By:

**🎯 SPLIT** → Divide data into groups
```python
# Split weather data by city
groups = df.groupby('city')
```

**🎯 APPLY** → Run calculations on each group
```python
# Find max temperature in each city
max_temps = groups['temperature'].max()
```

**🎯 COMBINE** → Merge results back together
```python
# Results automatically combined into one DataFrame
print(max_temps)
# Output:
# city
# Mumbai     92
# New York   36
# Paris      54
```

## **💡 Practical Examples from Transcript**

### **Example 1: Grouping Weather Data**
```python
import pandas as pd

# Read data
df = pd.read_csv('weather_by_cities.csv')
# Data looks like:
#   city      temperature  wind_speed
#   New York  32          6
#   Mumbai    90          9
#   Paris     45          15
#   New York  36          7
#   Mumbai    92          10
#   Paris     54          11

# Group by city
g = df.groupby('city')
```

### **Example 2: Basic Aggregations**
```python
# What's the maximum temperature in each city?
max_temps = g['temperature'].max()
# Mumbai: 92, New York: 36, Paris: 54

# Average wind speed in each city?
avg_wind = g['wind_speed'].mean()
# Mumbai: 9.5, New York: 6.5, Paris: 13

# Get ALL statistics at once
all_stats = g.describe()
# Shows count, mean, std, min, 25%, 50%, 75%, max
```

### **Example 3: Accessing Groups**
```python
# Method 1: Loop through groups
for city, city_data in g:
    print(f"City: {city}")
    print(f"Data:\n{city_data}\n")

# Method 2: Get specific group
mumbai_data = g.get_group('Mumbai')
# Returns only Mumbai rows as a DataFrame
```

## **🚀 Real-World Applications**

### **Use Case 1: Business Sales Analysis**
```python
# Group sales by region
sales_by_region = sales_data.groupby('region')

# Find total sales per region
total_sales = sales_by_region['revenue'].sum()

# Average transaction value per region
avg_transaction = sales_by_region['revenue'].mean()

# Number of customers per region
customer_count = sales_by_region['customer_id'].nunique()
```

### **Use Case 2: Student Performance**
```python
# Group students by grade
students_by_grade = students.groupby('grade')

# Average score in each grade
average_scores = students_by_grade['score'].mean()

# Highest score in each grade
top_scores = students_by_grade['score'].max()

# Number of students per grade
student_count = students_by_grade.size()
```

### **Use Case 3: Time-Based Analysis**
```python
# Convert date column to datetime
df['date'] = pd.to_datetime(df['date'])

# Group by month
df['month'] = df['date'].dt.month
monthly_data = df.groupby('month')

# Monthly averages
monthly_avg = monthly_data['value'].mean()
```

## **✨ Advanced Tips & Tricks**

### **1. Multiple Grouping Columns**
```python
# Group by both city AND day
g = df.groupby(['city', 'day'])

# Get maximum temperature for each city on each day
result = g['temperature'].max()
```

### **2. Different Aggregations per Column**
```python
# Different calculations for different columns
summary = df.groupby('city').agg({
    'temperature': ['max', 'min', 'mean'],
    'wind_speed': ['mean', 'std'],
    'humidity': 'mean'
})
```

### **3. Filter Groups**
```python
# Only keep groups with more than 5 rows
large_groups = g.filter(lambda x: len(x) > 5)

# Groups where average temperature > 30
hot_cities = g.filter(lambda x: x['temperature'].mean() > 30)
```

## **⚠️ Common Mistakes & Solutions**

| **Problem** | **Solution** |
|------------|--------------|
| Forgetting groupby creates an object, not DataFrame | Use aggregation methods: `.sum()`, `.mean()`, etc. |
| Grouping by wrong column | Check column names: `df.columns` |
| Not resetting index after groupby | Use `.reset_index()` to get clean DataFrame |
| Trying to plot groupby object directly | Aggregate first, then plot |

## **📊 Visualization Example**
```python
import matplotlib.pyplot as plt

# Simple groupby plot
df.groupby('city')['temperature'].mean().plot(kind='bar')
plt.title('Average Temperature by City')
plt.ylabel('Temperature (°C)')
plt.show()
```

## **🎯 Quick Reference Cheat Sheet**

```python
# BASIC SYNTAX
grouped = df.groupby('column')

# COMMON OPERATIONS
grouped.size()          # Count rows in each group
grouped.count()         # Count non-null values
grouped.sum()           # Sum of values
grouped.mean()          # Average
grouped.median()        # Median
grouped.std()           # Standard deviation
grouped.min()           # Minimum
grouped.max()           # Maximum
grouped.first()         # First value
grouped.last()          # Last value
grouped.nunique()       # Number of unique values

# ACCESSING
grouped.get_group('name')  # Get specific group
list(grouped.groups.keys()) # Get group names

# ITERATION
for name, group in grouped:
    print(name)
    print(group)
```

## **💡 Simple Analogy to Remember**

Think of **Group By** like organizing a **fruit basket**:
- **Step 1 (Split)**: Separate apples, oranges, bananas into different bowls
- **Step 2 (Apply)**: Count how many in each bowl / weigh each bowl
- **Step 3 (Combine)**: Write results: "Apples: 5, Oranges: 3, Bananas: 7"

**In code**:
```python
# Our fruit data
fruits = pd.DataFrame({
    'type': ['apple', 'orange', 'apple', 'banana', 'orange', 'apple'],
    'weight': [150, 120, 130, 200, 110, 140]
})

# Group by fruit type
fruit_groups = fruits.groupby('type')

# Count each fruit type
fruit_counts = fruit_groups.size()
# Result: apple: 3, orange: 2, banana: 1

# Average weight per fruit type
avg_weight = fruit_groups['weight'].mean()
# Result: average apple weight, average orange weight, etc.
```

**Key Takeaway**: Group By helps you **answer questions about categories** in your data - whether it's "average temperature per city" or "total sales per region" or "best student per class". It's one of the most powerful tools for data analysis in pandas! 🚀