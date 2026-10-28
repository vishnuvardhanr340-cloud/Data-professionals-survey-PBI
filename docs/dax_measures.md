# DAX Measures

All measures use the table `Data Professional Survey`.

## Core

```dax
Total respondents = COUNTROWS('Data Professional Survey')
```

```dax
Average Salary = AVERAGE('Data Professional Survey'[Average Salary])
```

```dax
Median Salary = MEDIAN('Data Professional Survey'[Average Salary])
```

```dax
% career switchers =
DIVIDE(
    CALCULATE(COUNTROWS('Data Professional Survey'), 'Data Professional Survey'[Switch] = "Yes"),
    [Total respondents]
)
```

## Gender comparison

```dax
Avg Salary Male =
CALCULATE([Average Salary], 'Data Professional Survey'[Gender] = "Male")
```

```dax
Avg Salary Female =
CALCULATE([Average Salary], 'Data Professional Survey'[Gender] = "Female")
```

```dax
% Salary gap =
DIVIDE([Avg Salary Male] - [Avg Salary Female], [Average Salary])
```

A negative value means women's average salary is higher than men's in this sample.

## Ranking

```dax
Industry Salary Rank =
RANKX(ALL('Data Professional Survey'[Industry]), [Average Salary])
```

## Happiness

```dax
Avg Happiness =
DIVIDE(
    SUM('Data Professional Survey'[Hapiness- Salary]) + SUM('Data Professional Survey'[Happiness- Coworkers])
      + SUM('Data Professional Survey'[Happiness- Management]) + SUM('Data Professional Survey'[Happiness- Upward Mobility])
      + SUM('Data Professional Survey'[Happiness- Work/Life Balance]),
    COUNT('Data Professional Survey'[Hapiness- Salary]) + COUNT('Data Professional Survey'[Happiness- Coworkers])
      + COUNT('Data Professional Survey'[Happiness- Management]) + COUNT('Data Professional Survey'[Happiness- Upward Mobility])
      + COUNT('Data Professional Survey'[Happiness- Work/Life Balance])
)
```

This measure averages five of the six happiness factors; Learning New Things is not included.

```dax
Avg Happy Salary = AVERAGE('Data Professional Survey'[Hapiness- Salary])
Avg Happiness Coworkers = AVERAGE('Data Professional Survey'[Happiness- Coworkers])
Avg Happiness Management = AVERAGE('Data Professional Survey'[Happiness- Management])
Avg Happiness Upward Mobility = AVERAGE('Data Professional Survey'[Happiness- Upward Mobility])
Avg Happiness worklife = AVERAGE('Data Professional Survey'[Happiness- Work/Life Balance])
```
