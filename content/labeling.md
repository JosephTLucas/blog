# Data Labeling Tip

I have spent a lot of time labeling lately, and I have two guiding principles:
1. Where you can, automatically label.
2. Make it easy to correct automatic labels.

*Automatically Label*

If you had a perfect labeling oracle, you probably would not need to be training a supervised classification model; you would already have an unsupervised model. But you may have a strongly correlated feature or other algorithm that can label your data with some degree of uncertainty. Take this win when you can. Use some substandard method to generate the majority of the labels for you, then spend your work-hours cleaning them up (instead of generating them from scratch). For my main use case, [peak detection](https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.find_peaks.html) labeled about 70% accurately. This isn't an acceptable accuracy for production, but it is good enough to save me some time.

*Correct Labels*

Next, I recommend [matplotlib's jupyter extension](https://github.com/matplotlib/ipympl) and [event handling](https://matplotlib.org/3.3.1/users/event_handling.html) to do your label correction.

1. Use your labeling oracle to generate a list of labels and their location. For a binary classification task on time series data, I just used the index of each positive class prediction.
2. Plot these label predictions over your data stream.
3. Use the interactive plot to scroll and zoom through your data.
4. Assign matplotlib events to add or remove labels from your label list. In this example, we use the `z` key to add labels and the `x` key to remove labels (at the mouseover location).
```python
add_list = []
remove_list = []
def onkey(event):
	if event.key == 'z':
		add_list.append(round(event.xdata))
	if event.key == 'x':
		remove_list.append(round(event.xdata))

f.canvas.mpl_connect('key_press_event', onkey)
```
5. Afterwards, some list operations allow you to add and remove the necessary labels.

You can see how defining other events would enable you to extend this example to a multiclass problem. Likewise, further defining the coordinate system would enable you to extend this to labeling two-dimensional clusters.
