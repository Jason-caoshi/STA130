```python
import pandas as pd
url = " https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv"
df = pd.read_csv(url)
df.isna().sum()

# Check for missing values in the entire DataFrame
missing_values = df.isnull().sum()

print("Missing values in each column:")
print(missing_values)

# Check if there are any missing values at all
if df.isnull().values.any():
    print("\nThe dataset contains missing values.")
else:
    print("\nThe dataset has no missing values.")

```

    Missing values in each column:
    survived         0
    pclass           0
    sex              0
    age            177
    sibsp            0
    parch            0
    fare             0
    embarked         2
    class            0
    who              0
    adult_male       0
    deck           688
    embark_town      2
    alive            0
    alone            0
    dtype: int64
    
    The dataset contains missing values.



```python

```

#2


```python
import pandas as pd


df = pd.DataFrame(df)

# Get the number of rows and columns
num_rows, num_columns = df.shape

print(f"The DataFrame has {num_rows} rows and {num_columns} columns.")
```

    The DataFrame has 891 rows and 15 columns.


#2 "observation" : observation refers to instances in the dataset, where values were measured/observed for all variables. Observations are often the "rows" of a dataframe
In the example about, each observation is each person who were abaord titanic when it sunk

"variables" : variables are what are being measured/observed, they are usually the columns of a dataframe
In the example, the variables are "survived", "pclass", "sex", "age", etc



```python
print("Shape of the DataFrame:")
print(df.shape)  # This will print a tuple (number of rows, number of columns)

# Use df.describe() to get summary statistics of numerical columns
print("\nSummary statistics with df.describe():")
print(df.describe())

# Use df.describe(include=['object']) to get summary statistics of categorical columns
print("\nSummary statistics of categorical columns with df.describe(include=['object']):")
print(df.describe(include=['object']))
```

    Shape of the DataFrame:
    (891, 15)
    
    Summary statistics with df.describe():
             survived      pclass         age       sibsp       parch        fare
    count  891.000000  891.000000  714.000000  891.000000  891.000000  891.000000
    mean     0.383838    2.308642   29.699118    0.523008    0.381594   32.204208
    std      0.486592    0.836071   14.526497    1.102743    0.806057   49.693429
    min      0.000000    1.000000    0.420000    0.000000    0.000000    0.000000
    25%      0.000000    2.000000   20.125000    0.000000    0.000000    7.910400
    50%      0.000000    3.000000   28.000000    0.000000    0.000000   14.454200
    75%      1.000000    3.000000   38.000000    1.000000    0.000000   31.000000
    max      1.000000    3.000000   80.000000    8.000000    6.000000  512.329200
    
    Summary statistics of categorical columns with df.describe(include=['object']):
             sex embarked  class  who deck  embark_town alive
    count    891      889    891  891  203          889   891
    unique     2        3      3    3    7            3     2
    top     male        S  Third  man    C  Southampton    no
    freq     577      644    491  537   59          644   549


#4 df.shape only gives you how many row/columns while df.describe() gives details about what's in each column, giving you the count, mean, std, min... max of the column. 
But df.describe will only be able to give you summary for numerical column
While df.shape gives you the full dimension of the data frame, df.describe() will skips the missing values, (as you can see under age/count), even tho there are 891 rows, df.describe only counted 714 under age. 
Also df.shape is an attribute that doesn't require Parentheses while df.describe() is a function that does require parentheses  

#5 attributes variables that are associated with an object, it is used to hold data about the object, and it is accessed by using dot notation without paraenthese
on the other hand
methods are actions that are assoicated with an object, it is used to perform certain operations on the object, it can be called also using dot notation but with paraenthese after it to include arguments

#6 count: the number of non missing value in the column
mean: the average of the non missing value in the column
std: the standard deviation of the non missing value in the column
min: the lowest value in the column
25%: 25th percentile of the data, or Q1
50%: 50th percentile of the data, or mediumn 
75%: 75th percentile of the data, or Q3
max: the highest value int he column


#7 
1. you might find "df.dropna()" a better method than "del df['col']" when you don't want to permanently delete an entire column
2. you might want to use "del df['col']" when you want to delete a specific column rather than just the ones with missing value
3. You might want to apply "del df['col']" before you use "df.dropna()" when you want to remove specific data from the dataframe before you removing the missing values, since having missing values in the column may affect whcih row/column "df.dropna" with drop



```python
print(df)
del df['deck']
del df['age']
df.dropna()
print(df)
```

         survived  pclass     sex   age  sibsp  parch     fare embarked   class  \
    0           0       3    male  22.0      1      0   7.2500        S   Third   
    1           1       1  female  38.0      1      0  71.2833        C   First   
    2           1       3  female  26.0      0      0   7.9250        S   Third   
    3           1       1  female  35.0      1      0  53.1000        S   First   
    4           0       3    male  35.0      0      0   8.0500        S   Third   
    ..        ...     ...     ...   ...    ...    ...      ...      ...     ...   
    886         0       2    male  27.0      0      0  13.0000        S  Second   
    887         1       1  female  19.0      0      0  30.0000        S   First   
    888         0       3  female   NaN      1      2  23.4500        S   Third   
    889         1       1    male  26.0      0      0  30.0000        C   First   
    890         0       3    male  32.0      0      0   7.7500        Q   Third   
    
           who  adult_male deck  embark_town alive  alone  
    0      man        True  NaN  Southampton    no  False  
    1    woman       False    C    Cherbourg   yes  False  
    2    woman       False  NaN  Southampton   yes   True  
    3    woman       False    C  Southampton   yes  False  
    4      man        True  NaN  Southampton    no   True  
    ..     ...         ...  ...          ...   ...    ...  
    886    man        True  NaN  Southampton    no   True  
    887  woman       False    B  Southampton   yes   True  
    888  woman       False  NaN  Southampton    no  False  
    889    man        True    C    Cherbourg   yes   True  
    890    man        True  NaN   Queenstown    no   True  
    
    [891 rows x 15 columns]
         survived  pclass     sex  sibsp  parch     fare embarked   class    who  \
    0           0       3    male      1      0   7.2500        S   Third    man   
    1           1       1  female      1      0  71.2833        C   First  woman   
    2           1       3  female      0      0   7.9250        S   Third  woman   
    3           1       1  female      1      0  53.1000        S   First  woman   
    4           0       3    male      0      0   8.0500        S   Third    man   
    ..        ...     ...     ...    ...    ...      ...      ...     ...    ...   
    886         0       2    male      0      0  13.0000        S  Second    man   
    887         1       1  female      0      0  30.0000        S   First  woman   
    888         0       3  female      1      2  23.4500        S   Third  woman   
    889         1       1    male      0      0  30.0000        C   First    man   
    890         0       3    male      0      0   7.7500        Q   Third    man   
    
         adult_male  embark_town alive  alone  
    0          True  Southampton    no  False  
    1         False    Cherbourg   yes  False  
    2         False  Southampton   yes   True  
    3         False  Southampton   yes  False  
    4          True  Southampton    no   True  
    ..          ...          ...   ...    ...  
    886        True  Southampton    no   True  
    887       False  Southampton   yes   True  
    888       False  Southampton    no  False  
    889        True    Cherbourg   yes   True  
    890        True   Queenstown    no   True  
    
    [891 rows x 13 columns]



```python
missing_values = df.isnull().sum()

print("Missing values in each column:")
print(missing_values)

# Check if there are any missing values at all
if df.isnull().values.any():
    print("\nThe dataset contains missing values.")
else:
    print("\nThe dataset has no missing values.")
```

#8 df.groupby('col1')['col2'].describe() will create a new dataframe for each unique value in 'col1' and assign all the values in 'col2' to the new groups, then it would run the usual .describe() for each of the new group, giving you the count, mean, std, min, etc

I will do an example below, using 'deck' and 'fare'


```python
df.groupby('deck')['fare'].describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>deck</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>15.0</td>
      <td>39.623887</td>
      <td>17.975333</td>
      <td>0.0000</td>
      <td>30.8479</td>
      <td>35.50000</td>
      <td>50.24790</td>
      <td>81.8583</td>
    </tr>
    <tr>
      <th>B</th>
      <td>47.0</td>
      <td>113.505764</td>
      <td>109.301500</td>
      <td>0.0000</td>
      <td>57.0000</td>
      <td>80.00000</td>
      <td>120.00000</td>
      <td>512.3292</td>
    </tr>
    <tr>
      <th>C</th>
      <td>59.0</td>
      <td>100.151341</td>
      <td>70.225588</td>
      <td>26.5500</td>
      <td>42.5021</td>
      <td>83.47500</td>
      <td>143.59165</td>
      <td>263.0000</td>
    </tr>
    <tr>
      <th>D</th>
      <td>33.0</td>
      <td>57.244576</td>
      <td>29.592832</td>
      <td>12.8750</td>
      <td>30.0000</td>
      <td>53.10000</td>
      <td>77.28750</td>
      <td>113.2750</td>
    </tr>
    <tr>
      <th>E</th>
      <td>32.0</td>
      <td>46.026694</td>
      <td>32.608315</td>
      <td>8.0500</td>
      <td>26.1125</td>
      <td>45.18125</td>
      <td>56.15730</td>
      <td>134.5000</td>
    </tr>
    <tr>
      <th>F</th>
      <td>13.0</td>
      <td>18.696792</td>
      <td>11.728217</td>
      <td>7.6500</td>
      <td>7.7500</td>
      <td>13.00000</td>
      <td>26.00000</td>
      <td>39.0000</td>
    </tr>
    <tr>
      <th>G</th>
      <td>4.0</td>
      <td>13.581250</td>
      <td>3.601222</td>
      <td>10.4625</td>
      <td>10.4625</td>
      <td>13.58125</td>
      <td>16.70000</td>
      <td>16.7000</td>
    </tr>
  </tbody>
</table>
</div>



Rather than showing just how much missing data there are, the count also shows the amount of elements in each new group

#8.3


```python
df
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Cell In[1], line 1
    ----> 1 df


    NameError: name 'df' is not defined



```python
import pandas as pd
url = " https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanics.csv"
df = pd.read_csv(url)
```


    ---------------------------------------------------------------------------

    HTTPError                                 Traceback (most recent call last)

    Cell In[1], line 3
          1 import pandas as pd
          2 url = " https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanics.csv"
    ----> 3 df = pd.read_csv(url)


    File /opt/conda/lib/python3.11/site-packages/pandas/io/parsers/readers.py:948, in read_csv(filepath_or_buffer, sep, delimiter, header, names, index_col, usecols, dtype, engine, converters, true_values, false_values, skipinitialspace, skiprows, skipfooter, nrows, na_values, keep_default_na, na_filter, verbose, skip_blank_lines, parse_dates, infer_datetime_format, keep_date_col, date_parser, date_format, dayfirst, cache_dates, iterator, chunksize, compression, thousands, decimal, lineterminator, quotechar, quoting, doublequote, escapechar, comment, encoding, encoding_errors, dialect, on_bad_lines, delim_whitespace, low_memory, memory_map, float_precision, storage_options, dtype_backend)
        935 kwds_defaults = _refine_defaults_read(
        936     dialect,
        937     delimiter,
       (...)
        944     dtype_backend=dtype_backend,
        945 )
        946 kwds.update(kwds_defaults)
    --> 948 return _read(filepath_or_buffer, kwds)


    File /opt/conda/lib/python3.11/site-packages/pandas/io/parsers/readers.py:611, in _read(filepath_or_buffer, kwds)
        608 _validate_names(kwds.get("names", None))
        610 # Create the parser.
    --> 611 parser = TextFileReader(filepath_or_buffer, **kwds)
        613 if chunksize or iterator:
        614     return parser


    File /opt/conda/lib/python3.11/site-packages/pandas/io/parsers/readers.py:1448, in TextFileReader.__init__(self, f, engine, **kwds)
       1445     self.options["has_index_names"] = kwds["has_index_names"]
       1447 self.handles: IOHandles | None = None
    -> 1448 self._engine = self._make_engine(f, self.engine)


    File /opt/conda/lib/python3.11/site-packages/pandas/io/parsers/readers.py:1705, in TextFileReader._make_engine(self, f, engine)
       1703     if "b" not in mode:
       1704         mode += "b"
    -> 1705 self.handles = get_handle(
       1706     f,
       1707     mode,
       1708     encoding=self.options.get("encoding", None),
       1709     compression=self.options.get("compression", None),
       1710     memory_map=self.options.get("memory_map", False),
       1711     is_text=is_text,
       1712     errors=self.options.get("encoding_errors", "strict"),
       1713     storage_options=self.options.get("storage_options", None),
       1714 )
       1715 assert self.handles is not None
       1716 f = self.handles.handle


    File /opt/conda/lib/python3.11/site-packages/pandas/io/common.py:718, in get_handle(path_or_buf, mode, encoding, compression, memory_map, is_text, errors, storage_options)
        715     codecs.lookup_error(errors)
        717 # open URLs
    --> 718 ioargs = _get_filepath_or_buffer(
        719     path_or_buf,
        720     encoding=encoding,
        721     compression=compression,
        722     mode=mode,
        723     storage_options=storage_options,
        724 )
        726 handle = ioargs.filepath_or_buffer
        727 handles: list[BaseBuffer]


    File /opt/conda/lib/python3.11/site-packages/pandas/io/common.py:372, in _get_filepath_or_buffer(filepath_or_buffer, encoding, compression, mode, storage_options)
        370 # assuming storage_options is to be interpreted as headers
        371 req_info = urllib.request.Request(filepath_or_buffer, headers=storage_options)
    --> 372 with urlopen(req_info) as req:
        373     content_encoding = req.headers.get("Content-Encoding", None)
        374     if content_encoding == "gzip":
        375         # Override compression based on Content-Encoding header


    File /opt/conda/lib/python3.11/site-packages/pandas/io/common.py:274, in urlopen(*args, **kwargs)
        268 """
        269 Lazy-import wrapper for stdlib urlopen, as that imports a big chunk of
        270 the stdlib.
        271 """
        272 import urllib.request
    --> 274 return urllib.request.urlopen(*args, **kwargs)


    File /opt/conda/lib/python3.11/urllib/request.py:216, in urlopen(url, data, timeout, cafile, capath, cadefault, context)
        214 else:
        215     opener = _opener
    --> 216 return opener.open(url, data, timeout)


    File /opt/conda/lib/python3.11/urllib/request.py:525, in OpenerDirector.open(self, fullurl, data, timeout)
        523 for processor in self.process_response.get(protocol, []):
        524     meth = getattr(processor, meth_name)
    --> 525     response = meth(req, response)
        527 return response


    File /opt/conda/lib/python3.11/urllib/request.py:634, in HTTPErrorProcessor.http_response(self, request, response)
        631 # According to RFC 2616, "2xx" code indicates that the client's
        632 # request was successfully received, understood, and accepted.
        633 if not (200 <= code < 300):
    --> 634     response = self.parent.error(
        635         'http', request, response, code, msg, hdrs)
        637 return response


    File /opt/conda/lib/python3.11/urllib/request.py:563, in OpenerDirector.error(self, proto, *args)
        561 if http_err:
        562     args = (dict, 'default', 'http_error_default') + orig_args
    --> 563     return self._call_chain(*args)


    File /opt/conda/lib/python3.11/urllib/request.py:496, in OpenerDirector._call_chain(self, chain, kind, meth_name, *args)
        494 for handler in handlers:
        495     func = getattr(handler, meth_name)
    --> 496     result = func(*args)
        497     if result is not None:
        498         return result


    File /opt/conda/lib/python3.11/urllib/request.py:643, in HTTPDefaultErrorHandler.http_error_default(self, req, fp, code, msg, hdrs)
        642 def http_error_default(self, req, fp, code, msg, hdrs):
    --> 643     raise HTTPError(req.full_url, code, msg, hdrs, fp)


    HTTPError: HTTP Error 404: Not Found



```python
import pandas as pd
url = " https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv"
df = pd.read_csv(url)
DF.groupby("col1")["col2"].describe()
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    Cell In[4], line 4
          2 url = " https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv"
          3 df = pd.read_csv(url)
    ----> 4 DF.groupby("col1")["col2"].describe()


    File /opt/conda/lib/python3.11/site-packages/pandas/core/frame.py:8869, in DataFrame.groupby(self, by, axis, level, as_index, sort, group_keys, observed, dropna)
       8866 if level is None and by is None:
       8867     raise TypeError("You have to supply one of 'by' and 'level'")
    -> 8869 return DataFrameGroupBy(
       8870     obj=self,
       8871     keys=by,
       8872     axis=axis,
       8873     level=level,
       8874     as_index=as_index,
       8875     sort=sort,
       8876     group_keys=group_keys,
       8877     observed=observed,
       8878     dropna=dropna,
       8879 )


    File /opt/conda/lib/python3.11/site-packages/pandas/core/groupby/groupby.py:1278, in GroupBy.__init__(self, obj, keys, axis, level, grouper, exclusions, selection, as_index, sort, group_keys, observed, dropna)
       1275 self.dropna = dropna
       1277 if grouper is None:
    -> 1278     grouper, exclusions, obj = get_grouper(
       1279         obj,
       1280         keys,
       1281         axis=axis,
       1282         level=level,
       1283         sort=sort,
       1284         observed=False if observed is lib.no_default else observed,
       1285         dropna=self.dropna,
       1286     )
       1288 if observed is lib.no_default:
       1289     if any(ping._passed_categorical for ping in grouper.groupings):


    File /opt/conda/lib/python3.11/site-packages/pandas/core/groupby/grouper.py:1009, in get_grouper(obj, key, axis, level, sort, observed, validate, dropna)
       1007         in_axis, level, gpr = False, gpr, None
       1008     else:
    -> 1009         raise KeyError(gpr)
       1010 elif isinstance(gpr, Grouper) and gpr.key is not None:
       1011     # Add key to exclusions
       1012     exclusions.add(gpr.key)


    KeyError: 'col1'



```python
import pandas as pd
url = " https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv"
df = pd.read_csv(url)
df.group_by("col1")["col2"].describe()
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    /tmp/ipykernel_52/28724748.py in ?()
          1 import pandas as pd
          2 url = " https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv"
          3 df = pd.read_csv(url)
    ----> 4 df.group_by("col1")["col2"].describe()
    

    /opt/conda/lib/python3.11/site-packages/pandas/core/generic.py in ?(self, name)
       6200             and name not in self._accessors
       6201             and self._info_axis._can_hold_identifiers_and_holds_name(name)
       6202         ):
       6203             return self[name]
    -> 6204         return object.__getattribute__(self, name)
    

    AttributeError: 'DataFrame' object has no attribute 'group_by'



```python
import pandas as pd
url = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv"
df = pd.read_csv(url)
df.groupby("deck")["Fare"].describe()
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    Cell In[9], line 4
          2 url = " https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv"
          3 df = pd.read_csv(url)
    ----> 4 df.groupby("deck")["Fare"].describe()


    File /opt/conda/lib/python3.11/site-packages/pandas/core/groupby/generic.py:1964, in DataFrameGroupBy.__getitem__(self, key)
       1957 if isinstance(key, tuple) and len(key) > 1:
       1958     # if len == 1, then it becomes a SeriesGroupBy and this is actually
       1959     # valid syntax, so don't raise
       1960     raise ValueError(
       1961         "Cannot subset columns with a tuple with more than one element. "
       1962         "Use a list instead."
       1963     )
    -> 1964 return super().__getitem__(key)


    File /opt/conda/lib/python3.11/site-packages/pandas/core/base.py:244, in SelectionMixin.__getitem__(self, key)
        242 else:
        243     if key not in self.obj:
    --> 244         raise KeyError(f"Column not found: {key}")
        245     ndim = self.obj[key].ndim
        246     return self._gotitem(key, ndim=ndim)


    KeyError: 'Column not found: Fare'



```python
import pandas as pd
url = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv"
df = pd.read_csv(url)
df.groupby("deck")[fare].describe()

```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Cell In[10], line 4
          2 url = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/titanic.csv"
          3 df = pd.read_csv(url)
    ----> 4 df.groupby("deck")[fare].describe()


    NameError: name 'fare' is not defined


After experimenting with both google and chatgpt to troubleshoot the codes above, I find that using chat was a lot faster at pin pointing exactly where the code when wrong and it also provided the correct code for me to try them out. Chat gpt also gives you explanation on what was the mistake and why the code needs to be changed

Using google is similar, but I couldn't just copy and paste my code into the brower, and it requires a bit of thinking and scrolling through the error messages. But often, the error message will give you a clear idea on what and where the code went wrong. Instead of giving you the correct code, searching on google will require you to understand what the error message is saying and how to fix it. It may take some work but it gives you a better understanding so you can better handle it next time. 

Overall, both methods are great, but chatgpt is a lot faster and straight forward. And since it has history of your code and exact dataset you are working with. It can come up with code for your situation while google will only teach you the ways to fix the code. 



#9 mostly

ChatGPT links: 
frist chat: https://chatgpt.com/share/66e37ce7-134c-8010-a722-b2581a55ca9a
Second chat: https://chatgpt.com/share/66e37cb8-33e4-8010-b94c-1b91ab15f7da
