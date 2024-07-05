```python
import matplotlib.pyplot as plt

"generate subplots in figure 1 : scatter([1,2][1,2])"
f, ((ax00, ax01),(ax10, ax11)) = plt.subplots(2,2, sharex=True, sharey=True) # create figure1, divide into 2x2 blocks, all blocks share xaxis and yaxis | save [figure1, blocks] to [f, ((ax00, ax01),(ax10, ax11))]	# ax00 = block in (0,0)
ax00.scatter([1,2],[1,2])  # generate scatter with [1,2],[1,2] in block of ax00

"optimize the layout of subplots "
plt.tight_layout()

"show figures"
plt.show()
```
