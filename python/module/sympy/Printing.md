#  Printers
## pretty printer
use unicode pretty printer by default
```python
init_printing()
```
use ASCII Pretty Printer by default
```python
init_printing(use_unicode=False)
```
- ASCII Pretty Printer
if the terminal doesn't support Unicode or doesn't print well, you can use this printer
```python
pprint(Integral(sqrt(1/x), x), use_unicode=False)
```
- Unicode Pretty Printer
```python
## Normally
pprint(Integral(sqrt(1/x), x))
## If the previous cmd dosen't work
pprint(Integral(sqrt(1/x), x), use_unicode=True)
```

## LaTex
```python
print(latex(Integral(sqrt(1/x), x)))
```

## MathML
```python
print_mathml(Integral(sqrt(1/x), x))
```