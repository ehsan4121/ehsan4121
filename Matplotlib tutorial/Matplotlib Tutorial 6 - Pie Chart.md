[![6](https://img.youtube.com/vi/GOuUGWGUT14/0.jpg)](https://www.youtube.com/watch?v=GOuUGWGUT14)

## **Important Concepts & Keywords Explained:**

### **1. Purpose of Pie Charts**
**What it means**: Pie charts show how different parts make up a whole. Like slicing a pizza to see what percentage each slice takes.
**Example from video**: Tracking home expenses to see what percentage goes to rent, food, etc.

### **2. Basic Pie Chart Syntax**
**What it means**: The simplest way to create a pie chart is `plt.pie(values, labels=labels)`.
```python
import matplotlib.pyplot as plt

expenses = [1400, 600, 300, 450, 250]  # Values
categories = ['Rent', 'Food', 'Gas', 'Utilities', 'Other']  # Labels

plt.pie(expenses, labels=categories)
plt.show()
```

### **3. Making It a Perfect Circle**
**What it means**: By default, pie charts might look oval-shaped. Use `plt.axis('equal')` to make it a perfect circle.
```python
plt.pie(expenses, labels=categories)
plt.axis('equal')  # Makes it a perfect circle
plt.show()
```

### **4. Showing Percentages (AutoPct)**
**What it means**: Automatically calculates and shows percentages on each slice.
```python
plt.pie(expenses, labels=categories, autopct='%1.1f%%')
# %1.1f%% means: show 1 decimal place (like 47.0%)
# %1.0f%% would show: 47% (no decimals)
```

### **5. Exploding Slices**
**What it means**: Pulling specific slices out from the center to highlight them.
```python
# To explode only the "Food" slice (2nd item):
explode_values = [0, 0.2, 0, 0, 0]  # 0 = no explode, 0.2 = pull out
plt.pie(expenses, labels=categories, explode=explode_values)
```

### **6. Changing Starting Angle**
**What it means**: Rotating where the first slice starts. Default is 0° (3 o'clock position).
```python
plt.pie(expenses, labels=categories, startangle=90)
# Starts at 90° (12 o'clock position)
```

### **7. Adding Shadows**
**What it means**: Adds a 3D-like shadow effect to make the chart look more polished.
```python
plt.pie(expenses, labels=categories, shadow=True)
```

### **8. Changing Chart Size**
**What it means**: Controls how big the pie chart appears.
```python
plt.pie(expenses, labels=categories, radius=1.5)  
# Default radius=1, 1.5 = 50% bigger
```

## **Step-by-Step Complete Example:**

```python
import matplotlib.pyplot as plt

# 1. Your data
expenses = [1400, 600, 300, 450, 250]
categories = ['Rent', 'Food', 'Gas', 'Utilities', 'Other']
explode = [0.1, 0, 0, 0, 0]  # Highlight Rent slice

# 2. Create pie chart with all features
plt.figure(figsize=(8, 6))  # Optional: Set figure size

plt.pie(expenses, 
        labels=categories,
        autopct='%1.1f%%',    # Show percentages with 1 decimal
        startangle=90,        # Start at top
        explode=explode,      # Pull out Rent slice
        shadow=True,          # Add shadow
        radius=1.2)           # Make it larger

plt.axis('equal')  # Perfect circle
plt.title('My Monthly Expenses')  # Add title
plt.show()
```

## **Real-World Applications:**

1. **Budget Tracking**: See where your money goes each month
2. **Survey Results**: Show percentage of people who chose different options
3. **Project Allocation**: Display how time/resources are distributed
4. **Market Share**: Visualize company shares in an industry

## **Pro Tips:**

- **Use limited slices**: Pie charts work best with 5-7 slices maximum
- **Order slices**: Put largest slice at top (use `startangle`)
- **Highlight important data**: Use `explode` for key slices
- **Add context**: Always include a title and clear labels
- **Consider alternatives**: For comparing many categories, bar charts might be better

## **Common Data Sources:**
The video mentions you can use:
- **Python lists** (like in the example)
- **Pandas DataFrames** (from CSV/Excel files)
- **NumPy arrays** (for numerical data)

## **Key Takeaways:**
1. Pie charts = visual breakdown of parts to whole
2. `plt.pie()` = main function, needs values and labels
3. `autopct` = shows percentages automatically
4. `explode` = highlights specific slices
5. `startangle` = rotates the chart
6. Always use `plt.axis('equal')` for perfect circles
7. Add `plt.show()` to display the chart cleanly

**Remember**: The power of pie charts is making percentages instantly understandable at a glance!