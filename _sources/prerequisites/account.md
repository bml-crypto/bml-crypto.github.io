---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---
(chapter1_part1)=

# 123




```{code-cell} ipython3
import numpy as np #to work with numbers
```

Next step is to re-create our hypothetical dataset that we've been working with:

```{code-cell} ipython3
x = np.array([[30], [46], [60], [65], [77], [95]])
y = np.array([31, 30, 80, 49, 70, 118])
print(x)
```
