Here are the key concepts and steps for reading and writing Excel/CSV files in pandas, explained simply with examples from the transcript.

### 📁 Basic Reading with `read_csv()` and `read_excel()`

These are your starting points to get data into pandas.

| Concept | What It Is | Example Code |
| :--- | :--- | :--- |
| **`read_csv()`** | Reads a CSV (Comma-Separated Values) file into a DataFrame. | `df = pd.read_csv('stock_data.csv')` |
| **`read_excel()`** | Reads an Excel file (.xlsx) into a DataFrame. | `df = pd.read_excel('data.xlsx', sheet_name='Sheet1')` |

**Think of it like this**: These commands work like opening a file in Excel, but instead of seeing it on a screen, the data is loaded into your Python program as a table (DataFrame) that you can work with.

### 🔧 Common & Useful Arguments for `read_csv()` / `read_excel()`

Files can be messy. These parameters help you clean up the data as you load it.

| Parameter | Why Use It? | How to Use It |
| :--- | :--- | :--- |
| **`skiprows`** | Skips unwanted rows at the **top** of the file (like extra titles or blank lines). | `pd.read_csv('file.csv', skiprows=1)` |
| **`header`** | • `header=1`: Use row number 1 as the column names.<br>• `header=None`: File has **no headers**. Pandas will use numbers (0,1,2...) as column names. | `pd.read_csv('file.csv', header=None)` |
| **`names`** | When you use `header=None`, use `names` to give your columns proper names. | `pd.read_csv('file.csv', header=None, names=['Ticker', 'EPS', 'Revenue'])` |
| **`nrows`** | Reads only a **specific number of data rows**. Great for quickly checking a huge file. | `pd.read_csv('big_file.csv', nrows=100)` |
| **`na_values`** | Tells pandas what values to treat as **missing data** (NaN). This is crucial for data cleaning. | `pd.read_csv('file.csv', na_values=['not available', 'n.a.', -1])` |

**Example**: If your CSV file has an unwanted title on the first line, and you know `"n.a."` means missing data, you would load it like this:
```python
df = pd.read_csv('messy_data.csv', skiprows=1, na_values=['n.a.'])
```

### ✍️ Writing Data with `to_csv()` and `to_excel()`

After you've cleaned or analyzed your data, save it back to a file.

| Function | What It Does | Common Arguments |
| :--- | :--- | :--- |
| **`df.to_csv()`** | Saves the DataFrame to a CSV file. | `df.to_csv('new_file.csv', index=False, columns=['Ticker', 'EPS'])` |
| **`df.to_excel()`** | Saves the DataFrame to an Excel file. | `df.to_excel('new_file.xlsx', sheet_name='Stocks', index=False)` |

**Key Arguments Explained**:
*   **`index=False`**: Tells pandas **not to save** the row numbers (the default index). You almost always want this when saving to a file for others to use.
*   **`columns=[...]`**: Lets you choose **only specific columns** to save.
*   **`sheet_name='...'`**: Names the sheet in your Excel file.

**Example**: Save only the 'Ticker' and 'Price' columns, without the index:
```python
df.to_csv('clean_data.csv', index=False, columns=['Ticker', 'Price'])
```

### 💡 Advanced and Handy Techniques

*   **Multiple DataFrames to One Excel File**: Use `pd.ExcelWriter` to write several DataFrames to different sheets in the same workbook.
    ```python
    with pd.ExcelWriter('report.xlsx') as writer:
        df_stocks.to_excel(writer, sheet_name='Stocks')
        df_weather.to_excel(writer, sheet_name='Weather')
    ```
*   **`converters` Argument**: Apply a custom function to clean a column **while reading** the file. For instance, you could replace all "n.a." entries in a "People" column with a specific name.
    ```python
    def clean_people(cell):
        return "Sam Walton" if cell == "n.a." else cell

    df = pd.read_excel('data.xlsx', converters={'People': clean_people})
    ```

### ✅ Key Takeaways
*   Use `read_csv()` and `read_excel()` to **import** your data.
*   Use `na_values` and `skiprows` to **clean messy data** right at the import stage.
*   Always use `index=False` when saving with `to_csv()` or `to_excel()` unless you need the index.
*   For complex Excel operations, like multiple sheets, use the `pd.ExcelWriter` tool.

Learn more on Glasp: https://glasp.co/reader?url=https://www.youtube.com/watch?v=-0NwrcZOKhQ