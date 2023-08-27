

# Pine Script

Pine Script is famouse scripting language used in trading view for various trading indicators, strategies or libraries.



## Indicators

Indicators are created using function `indicator`. It can have multiple arguments which can be passed to it like `title, offset etc.` 

```python
indicator(title = "Hello World!", shorttitle="IND", precision=2, format=format.volume)
plot(close)
```

- If `shorttitle` isn't passed then it will show value of title on the top left corner of the chart.



- Setting `overlay=true` in indicator will plot the indicator on chart otherwise it will plot the indicator in a seperate pane.

- Setting `format=format.volume` will make values in the specfic stock to a round figure in volume. e.g. if value of the indicator is 16234, than it will be displayed as 16.234k. There are other values to this argument like `format = format.price or format.percent` etc.

- Setting `scale=scale.left` or `scale.right`, `scale.none` will print the values of the scale in respective position.
- `max_bars_back=10` will calculate the indicator based on last 10 bars.
- `timeframe="5m"` will calculate the values based on 5 minute chart ignoring what time frame is opened in chart. It is good to use when you have time frame specific strategies.



**Price indicators**

<table>
    <tr>
    	<th>Title</th>
        <th>Variable used</th>
    </tr>
    <tr>
    	<td>Opening price</td>
        <td>open</td>
    </tr>
    <tr>
    	<td>Closing price</td>
        <td>close</td>
    </tr>
    <tr>
    	<td>Lowest price</td>
        <td>low</td>
    </tr>
    <tr>
    	<td>Highest price</td>
        <td>high</td>
    </tr>
    <tr>
    	<td>Opening price of nth previous bar</td>
        <td>open[10]</td>
    </tr>
</table>





## Plot

1. Plot:- plot function can only plot numbers

   - `title="Our Title"`
   - `color=color.blue`
   - `linewidth=2`
   - `style=plot.style._line`
   - `trackprice=true`: will create a line with current plot providing price information
   - `histbase=855`: will move the origin by 855 points or we can say that it created a new y-axis by setting 855 as base.
   - `offset=10`: will shift the plot to 10 units right. Setting it to negative value will shift it to left side.
   - `join=true`: if plot has shapes with space between them, it will join them by a line.
   - `editable=false` will prevent user from updating the indicator from indicator settings.
   - `show_last=20`: will only show last 20 plots of the indicator. **It won't affect the sample size of the calculation it is only related to visual effects**.
   - `display:display.none`: will hide the indicator. It is useful for debug purposes or if you want something to be visible if some condition is met.

   

**plotshape** function is similar to plot besides it can be used to create many shapes. It has different arguments like style, series, location, color. plotshape by default adds cross shape

```python
indicator(title="Average", overlay=true)
plotshape(close >= open, style=shape.triangleup, location=location.abovebar, color=color.green, size=size.huge)
plotshape(close <= open, style=shape.triangledown, location=location.belowbar, color=color.red, size=size.huge)
```



**plot** will be used to plot the given indicator on the chart. Plot also have many arguments like `plot(series=close, title = "plot title", color = color.red, linewidth = 2, style = plot.style_circles)`.

**Plotting on only last candle** can be done by using `plotshape(barstate.islast, .....)`.



## Libraries

There are several predefined libraries in pine. 

- Like **`ta`** (technical analysis) which contains all the indicators which one need for technical analysis. 
- A library for strings is also defined by the name of **`str`** which contains various functions on string like `length, format` etc.
- There is a library to define and test your strategies in pine by the name of **`strategy`**.
- **`request`** is a library which can be used to get data of the company like earnings, financials, dividends, splits etc.

## User Input

1. boolean input:- `bool_inp = input.bool("Are you above 18", defval=true)`. defval is default value.

   `boolean = input.bool(title = "Some boolean value", defval = true, tooltip = "Visible on Hover", confirm = true)`. Setting confirm to true will confirm from user when user adds a value.

2. Whole Number:- `number = input.int(minval = 5, maxval = 1000, step = 5, defval = 100)`

3. Float Number:- `float = input.float(defval = 12.20, maxval = 20.10, minval=10.05,)`

4. Price Input:- `buyPrice = input.price(defval = 0, title = "Entry Price", confirm = true)`: this is very different than other values as you have to click on the chart to set a value.
5. Time Input:- `time = input.time(defval = 0, title = "Select time on chart", confirm = true)`: this is similar to price input as you have to select a time on chart by clicking on it.



## Data Types

### Numbers

1. Integers:- `myInteger = 23`
2. Floats:- `myFloat = 12.85`

3. Boolean:- `myBool=true` `false`
4. Color:- `color.blue` or `#a1230d` or `color.rgb(123,82,72, 55)` last one is transperency
5. String:- `"This is pine script String"`

Data types can be also be defined by providing their type before declaring them like `float price = 65.45`. This is useful when we don't have a value and want to set a variable to null or `na` in pine script. This will only work if variable has a data type like `int count = na`.

If a variable is already declared and we want to update it we need to use `:=` instead of `=`.

When a new bar is created, whole script runs again. It will also redeclare all the variables we had declared before. To persist a variable from historic runs we need to set it's type to var. It is like creating a variable in global scope which doesn't die. `var persistance_count = 1`. **Simply a variable declared using var keyword will only be declared once, other times line will ignored**.



## Alerts

1. alert():- `alert(message="Price crossing " + str.toString(close), freq=alert.freq_all)`, **alert.freq_once_per_bar, alert.freq_once_per_bar_close.**
2. **alertCondition(boolean condition, title="Some Title", message="Some Message")**: In message we can use placeholder like: `{{open}}, {{close}}`.



## Plots Crossing

```python
// Get Emas
ema1 = ta.ema(close, 50)
ema2 = ta.ema(close, 100)

// Get Crosses
maCrossOver = ta.crossover(ema1, ema2) 
maCrossUnder = ta.crossunder(ema1, ema2)
maAnyCross = ta.cross(ema1, ema2)

// Draw emas
plot(ema1, color=color.red)
plot(ema2, color=color.blue)

// Change background color if cross happens
bgcolor(maCrossOver ? color.green: na)
bgcolor(maCrossUnder ? color.red: na)
```

