# This repo reproduces a bug in MCDP solver, where pessimistic estimation is **smaller** than optimistic estimation

Thanks @meshal-h for finding the bug!

## Description

When calling
```
mcdp-solve --imp --lower 100 --upper 100 continual_forecaster '<10 dimensionless>'
```

The output gives a result where the pessimistic estimation is **smaller** than the optimistic estimation.
This can be seen in the file `output/10.yaml`.
For other queries, like
```
mcdp-solve --imp --lower 100 --upper 100 continual_forecaster '<50 dimensionless>'
```
The result has no issue: pessimistic estimation is **larger** than the optimistic estimation

It seems the optimistic solution in `output/10.yaml` is abnormally large:

| Queried Functionality        | optimistic | pessimistic |
| :---------------- | :------: | ----: |
| 10 dimensionless        |   :warning: 187.07 USD :warning:  | 24.46 USD |
| 50 dimensionless           |   52.21 USD   | 90.95 USD |
| 90 dimensionless    |  239.43 USD   | 318.20 USD |

The branch `no-equality` has a version that only uses inequalities, but still produce the same results.

### Update by @meshal-h

The image `202409` gives same wrong optimistic estimation, **but** gives seemingly correct internal implementation.
The results are added to `output` folder with corresponding file names.
See the difference in the folllowing screenshot:
![image](https://github.com/user-attachments/assets/5cc004aa-8a05-4342-a5b2-a55da971709c)

