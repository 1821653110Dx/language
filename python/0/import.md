```python
import sales	# import module ./sales

sales.calc_tax()	# call sales's calc_tax()
```

```python
from sales import calc_shippling, calc_tax	# import func calc_shippling, calc_tax from module ./sales

calc_shipping()	# call imported calc_tax()
```

```python
import ecommerce.sales	# import module sales of package ./ecommerce

ecommers.sales.calc_tax()	# call ecommerce.sales's calc_tax()
```

```python
from ecommerce.sales import calc_tax	# import func cacl_tax from module sales of package ./ecoomerce

calc_tax()	# call imported calc_tax()
```

```python
from ecommerce import sales	# import module sales of package ./ecommerce

sales.calc_tax()	# call sales's calc_tax()
```

```python
from ..customer import contact	# import module contact from package ../customer
```

#   Path
```python
print(sys.path)	# newline print the path of module 'sys'
```