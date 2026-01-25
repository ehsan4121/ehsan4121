# **Pandas Melt Function: Complete Guide with Examples**

## **🎯 Key Concept: What is Melt?**
**Melt** is a pandas function that transforms **wide-format data** into **long-format data**. Think of it as "unpivoting" or "flattening" your data table.

### **Simple Analogy:**
Imagine you have a table like this (wide format):
| Day | New York | Chicago | Boston |
|-----|----------|---------|--------|
| Mon | 72°F     | 68°F    | 65°F   |
| Tue | 74°F     | 70°F    | 67°F   |

After melting, it becomes (long format):
| Day | City     | Temperature |
|-----|----------|-------------|
| Mon | New York | 72°F        |
| Mon | Chicago  | 68°F        |
| Mon | Boston   | 65°F        |
| Tue | New York | 74°F        |
| Tue | Chicago  | 70°F        |
| Tue | Boston   | 67°F        |

---

## **📊 Important Points & Keywords:**

### **1. When to Use Melt?** *(00:26)*
- **Transform data** for different types of analysis
- **Reshape data** from columns to rows
- When you need **each variable in its own row** for filtering/analysis
- **Useful for**: Data visualization, filtering specific categories, database storage

### **2. ID Variables** *(01:45)*
- **What**: Columns you want to **keep as identifiers** (don't want to melt)
- **Think of it as**: Your **x-axis** or primary keys
- **Example**: If melting city temperatures, keep "Day" as ID variable
```python
# Day stays as column, cities become rows
pd.melt(df, id_vars=['Day'])
```

### **3. Variable & Value Names** *(03:25)*
- **Default names**: 'variable' (for melted column names) and 'value' (for values)
- **Customize them**: Make your DataFrame more readable
```python
pd.melt(df, id_vars=['Day'], 
        var_name='City',      # Custom name for former column headers
        value_name='Temp')    # Custom name for values
```

### **4. The Transformation Process**
**Before Melt** (Wide format):
```python
import pandas as pd
df = pd.DataFrame({
    'Day': ['Mon', 'Tue', 'Wed'],
    'NY': [72, 74, 73],
    'Chicago': [68, 70, 69],
    'Boston': [65, 67, 66]
})
```
**Output:**
```
   Day  NY  Chicago  Boston
0  Mon  72       68      65
1  Tue  74       70      67
2  Wed  73       69      66
```

**After Melt** *(01:45)*:
```python
melted_df = pd.melt(df, id_vars=['Day'])
```
**Output:**
```
   Day variable  value
0  Mon       NY     72
1  Tue       NY     74
2  Wed       NY     73
3  Mon  Chicago     68
4  Tue  Chicago     70
5  Wed  Chicago     69
6  Mon   Boston     65
7  Tue   Boston     67
8  Wed   Boston     66
```

**With Custom Names** *(03:57)*:
```python
melted_df = pd.melt(df, id_vars=['Day'], 
                    var_name='City', 
                    value_name='Temperature')
```
**Output:**
```
   Day     City  Temperature
0  Mon       NY           72
1  Tue       NY           74
2  Wed       NY           73
3  Mon  Chicago           68
4  Tue  Chicago           70
5  Wed  Chicago           69
6  Mon   Boston           65
7  Tue   Boston           67
8  Wed   Boston           66
```

---

## **🔧 Practical Benefits & Use Cases:**

### **1. Easy Filtering** *(02:26)*
Once melted, filtering becomes much simpler:
```python
# Get only Chicago data
chicago_data = melted_df[melted_df['City'] == 'Chicago']
```

### **2. Better for Visualization**
Most plotting libraries prefer long-format data:
```python
import seaborn as sns
# Easy to create grouped plots with melted data
sns.lineplot(data=melted_df, x='Day', y='Temperature', hue='City')
```

### **3. Database Friendly**
Long format is more suitable for SQL databases and efficient storage.

---

## **📝 Real-World Examples:**

### **Example 1: Sales Data Transformation**
**Before** (Wide format - hard to analyze by product):
| Month | Product_A | Product_B | Product_C |
|-------|-----------|-----------|-----------|
| Jan   | $1000     | $1500     | $800      |
| Feb   | $1200     | $1600     | $900      |

**After melting:**
```python
melted_sales = pd.melt(sales_df, id_vars=['Month'],
                       var_name='Product',
                       value_name='Revenue')
```
**Now you can easily:**
- Compare products over time
- Find best/worst performing products
- Calculate total revenue per product

### **Example 2: Student Grades**
**Before melting:**
| Student | Math | Science | English |
|---------|------|---------|---------|
| Alice   | 95   | 88      | 92      |
| Bob     | 87   | 91      | 85      |

**After melting:**
```python
melted_grades = pd.melt(grades_df, id_vars=['Student'],
                        var_name='Subject',
                        value_name='Score')
```
**Now you can:**
- Find average score per subject
- Identify students struggling in specific subjects
- Compare performance across subjects

---

## **🚀 Pro Tips & Best Practices:**

1. **Always rename columns** after melting for clarity
2. **Choose ID variables carefully** - these should be your primary identifiers
3. **Melt is reversible** - use `pivot()` or `pivot_table()` to go back to wide format
4. **Check for duplicates** - melting can create duplicate rows if not careful
5. **Memory efficiency** - Long format can sometimes use more memory but is more flexible

---

## **🆚 Melt vs Pivot: Quick Comparison**

| **Aspect**       | **Melt (Unpivot)**              | **Pivot (Widen)**               |
|------------------|---------------------------------|---------------------------------|
| **Direction**    | Columns → Rows                  | Rows → Columns                  |
| **When to use**  | For analysis & filtering        | For reporting & presentation    |
| **Input**        | Wide format data                | Long format data                |
| **Output**       | Long format data                | Wide format data                |
| **Analogy**      | "Flatten" the table             | "Spread out" the table          |

---

## **💡 Key Takeaways:**

1. **Melt transforms wide → long format** (columns become rows)
2. **ID variables stay as columns** (they're your identifiers)
3. **Rename 'variable'/'value' columns** for better readability
4. **Melted data is easier to filter and analyze**
5. **Essential for preparing data for visualization and databases**

**Remember**: Melt doesn't destroy your original data - it creates a new transformed DataFrame that's often more useful for analysis!

Learn more on Glasp: https://glasp.co/reader?url=https://www.youtube.com/watch?v=oY62o-tBHF4