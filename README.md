---
jupyter:
  colab:
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

<div class="cell markdown" id="o4m72eEchiFK">

# CUHK-STAT1013:Practical Assignment Part 1

</div>

<div class="cell markdown" id="SAm7lUTUn8SU">

## Total bill dataset background

**Description**:

Dataset describing the total bill of a meal of individual customers.

**Github**:
<https://github.com/prasertcbs/basic-dataset/blob/d3e2b02215fcef95bfa29afe8b577c778656a479/seaborn/tips.csv>

**Sample size**: 244

**Feature documentation**:

| Feature    | Class      | Shape | Dtype   |
|:-----------|:-----------|:------|:--------|
| total_bill | Tensor     |       | float32 |
| tip        | Tensor     |       | float32 |
| sex        | ClassLabel |       | int64   |
| smoker     | ClassLabel |       | string  |
| day        | ClassLabel |       | string  |
| time       | ClassLabel |       | string  |
| size       | Tensor     |       | int64   |

</div>

<div class="cell markdown" id="ZfDEmHOLvuPm">

## Hypothesis

-   Idea
    -   We are interested in "Does women spend more in meals?"
-   What two groups are you comparing:
    -   **G1**:average total bill of male ; **G2**:average total bill of
        female
-   What you will be measuring:
    -   `total_bill`
-   Is your response variable quantitative rather than catergorical?
    -   `total_bill` is a quantitative variable
-   Make a prediction about what kind of difference you expect to see
    between your samples and why?
    -   We would expect **G1**\>**G2** since generally male requires a
        higher level of quality of life
-   Talk about how you will gather your data
    -   From Github link:
        <https://github.com/prasertcbs/basic-dataset/blob/d3e2b02215fcef95bfa29afe8b577c778656a479/seaborn/tips.csv>
-   If you had unlimited resources, how would you collect your data?
    -   i\) Attempt to collect more data; (ii) investigate if the
        provided dataset is a good random sampling subset of the
        original population

</div>

<div class="cell markdown" id="PWe8WjYlG9re">

## My Dataset

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:206}"
id="rOj1n_boxZUQ" outputId="26095e22-4067-453e-db58-a78bc74bb82a">

``` python
## load dataset from github

import pandas as pd

df = pd.read_csv('https://raw.githubusercontent.com/prasertcbs/basic-dataset/d3e2b02215fcef95bfa29afe8b577c778656a479/seaborn/tips.csv')
df.head(5)


```

<div class="output execute_result" execution_count="17">

       total_bill   tip     sex smoker  day    time  size
    0       16.99  1.01  Female     No  Sun  Dinner     2
    1       10.34  1.66    Male     No  Sun  Dinner     3
    2       21.01  3.50    Male     No  Sun  Dinner     3
    3       23.68  3.31    Male     No  Sun  Dinner     2
    4       24.59  3.61  Female     No  Sun  Dinner     4

</div>

</div>

<div class="cell markdown" id="c9yphY661u7X">

**G1** (total_bill \| sex = male) vs. **G2** (total_bill \| sex =
female)

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="4aGI8VsF3feO" outputId="fd511c4d-cacf-482c-afa0-adbc812c809f">

``` python
## First 5 records of G1 (Male)
(df[df['sex'] == 'Male']['total_bill']).head(5)
```

<div class="output execute_result" execution_count="12">

    1    10.34
    2    21.01
    3    23.68
    5    25.29
    6     8.77
    Name: total_bill, dtype: float64

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="QxpoKhcmlPaG" outputId="21409822-08c5-4541-87ef-eba11bf29bbb">

``` python
## First 5 records of G2 (Female)
(df[df['sex'] == 'Female']['total_bill']).head(5)
```

<div class="output execute_result" execution_count="4">

    0     16.99
    4     24.59
    11    35.26
    14    14.83
    16    10.33
    Name: total_bill, dtype: float64

</div>

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}"
id="QXQwXOm_Dj8G" outputId="821cb4f4-85f3-4bb2-ebe6-843c8914a9fb">

``` python
df.groupby('sex')['total_bill'].mean()
```

<div class="output execute_result" execution_count="13">

    sex
    Female    18.056897
    Male      20.744076
    Name: total_bill, dtype: float64

</div>

</div>

<div class="cell code" id="A6Ltm7QqBv39">

``` python
import matplotlib.pyplot as plt
import seaborn as sns
plt.rcParams['figure.figsize'] = [10,5]

sns.set()
```

</div>

<div class="cell code"
colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;,&quot;height&quot;:661}"
id="N5JP5lLN_SiG" outputId="7dff2466-21c1-4b00-c34a-ef212d4e611c">

``` python
sns.histplot(df, x='total_bill', hue='sex')
plt.show()

sns.violinplot(x=df['total_bill'])
plt.show()

```

<div class="output display_data">

![](2d51e71cd238997a7f94dc2ac8cb76d97279829c.png)

</div>

<div class="output display_data">

![](3768e899ea6adbdd794c85f3ce1686d30bbe5295.png)

</div>

</div>

<div class="cell markdown" id="7KEFjAwQEO1N">

**Open question**: Why do you think male generally spends more on their
meals?

</div>
