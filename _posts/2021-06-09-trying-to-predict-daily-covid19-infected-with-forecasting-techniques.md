Forecasting is the process of making predictions based on past and present data and most commonly by analysis of trends.
Forecast has applications in a wide range of fields where predict future it's useful. 
For example, in Supply Chain Management for enterprises that need an estimation of how many product, because they don't want to lose possible sales and also they don't want to product much more than real sales and thus increase profit margin.
Another example is the weather, because today, we want to know the weather of tomorrow or even whole week, in order to plan our day/week.
Also, forecasting has application in political elections. 
This examples are very known and establish how important is to make an acurrate forecast.

Forecast is not an easy problem, because the time component, ie, it's not a typical fitting problem. Because the data of today, could depend on yesterday data, 
but also whole week before, and moreover, in which proportions is it this dependence? maybe not all days has the same weight. 
Often the data has <strong>stationality</strong>. For example, sales of pools or ice creams increase at summer, and decrease at winter.
There is another forecast component, and this is the <strong>trend</strong>. Imagine a business that is doing very well, this would be like a linear function,
then the trend it's like the revenues are always increasing.

Now, we are going to apply some forecasting techniques in order to predict daily infected Covid-19 people in Chile (with real data, provided by the science ministery, https://www.minciencia.gob.cl/covid19/). For simplicity reasons, the analysis will be considering only one variable, the time (Time Series). If we wanted to improve the results, would be necessary to consider other variables (exogenous) like PCRs took each day or if there is restrictions or not. 

<h1> Naive forecast </h1>

The simplest model is the Naive forecast, that such as his name indicate, it's naive because try to forecast duplicating values. 
For example, to predict the daily Covid-19 infected people for tomorrow an options it's use the value of today. 
If we have certain knowledge about our data, we can improve this Naive forecast. In this case, we observe a week seasonality, 
if we want to predict tomorrow infected, we use the data of seven previous days.

<img src="https://raw.githubusercontent.com/RodrigoZelada/RodrigoZelada.github.io/master/images/naive.png" alt="hi" class="inline"/>

<h1> Moving average </h1>

Moving Average (MA) is an algorithm to smooth the fluctuations. The values are computed averaging in <i>windows</i> of data. 
For example, a Moving Average with $p=7$ days, it's that tomorrow prediction is computed averaging the seven previous days.

<img src="https://raw.githubusercontent.com/RodrigoZelada/RodrigoZelada.github.io/master/images/ma.png" alt="hi" class="inline"/>

<h1> Prophet </h1>

Prophet it's a powerful tool provided by Facebook. The main idea it's split the forecast components in trend, seasonality and residual.
To get more details, review <a href="https://peerj.com/preprints/3190.pdf">this article</a>.

<img src="https://raw.githubusercontent.com/RodrigoZelada/RodrigoZelada.github.io/master/images/prophet.png" width="500" height="250" alt="hi" class="inline"/>

<h1> Recurrent Neural Networks (RNN) - LSTM </h1>

Recurrent Neural Networks is a Deep Learning algorithm for fitting Time Series. It's recurrent because the "Seasonality".
In simple words, it's a neural network with a specific architecture. In particular, we use the LSTM algorithm, that stands for
<i>Long Short Term Memory</i> (there are others RNN algoritms like <i>GRU</i>).

We observe first the lost function, that it's crearly decreasing. The next figure it's the fitting, using the LSTM algorithm.

<img src="https://raw.githubusercontent.com/RodrigoZelada/RodrigoZelada.github.io/master/images/loss_function.png" alt="hi" class="inline"/>

<img src="https://raw.githubusercontent.com/RodrigoZelada/RodrigoZelada.github.io/master/images/tensorflow.png" alt="hi" class="inline"/>

<h1> Comparison </h1>

<table>
  <thead>
    <tr style="text-align: right;">
      <th>date</th>
      <th>daily_infected</th>
      <th>ma</th>
      <th>prophet</th>
      <th>RNN (tf)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2021-06-03</th>
      <td>8150</td>
      <td>7226</td>
      <td>6933</td>
      <td>8259</td>
    </tr>
    <tr>
      <th>2021-06-04</th>
      <td>8273</td>
      <td>7168</td>
      <td>7420</td>
      <td>8370</td>
    </tr>
    <tr>
      <th>2021-06-05</th>
      <td>8867</td>
      <td>7231</td>
      <td>7184</td>
      <td>8044</td>
    </tr>
    <tr>
      <th>2021-06-06</th>
      <td>7768</td>
      <td>7230</td>
      <td>6945</td>
      <td>7622</td>
    </tr>
    <tr>
      <th>2021-06-07</th>
      <td>6958</td>
      <td>7241</td>
      <td>6173</td>
      <td>5992</td>
    </tr>
    <tr>
      <th>2021-06-08</th>
      <td>5568</td>
      <td>7316</td>
      <td>4914</td>
      <td>4860</td>
    </tr>
    <tr>
      <th>2021-06-09</th>
      <td>5369</td>
      <td>7279</td>
      <td>5184</td>
      <td>5110</td>
    </tr>
   </tbody>
</table>


<img src="https://raw.githubusercontent.com/RodrigoZelada/RodrigoZelada.github.io/master/images/test.png" alt="hi" class="inline"/>

Mean error are respectively, Moving Average 1163.57, LST 443.72 and Prophet 885.08. This is consistent with what we observe in the figure, that LSTM with Tensorflow seems to be the most accurate.

<h1> Predictions for next week </h1>

<img src="https://raw.githubusercontent.com/RodrigoZelada/RodrigoZelada.github.io/master/images/predictions.png" alt="hi" class="inline"/>

<table>
  <thead>
    <tr style="text-align: right;">
      <th>date</th>
      <th>ma</th>
      <th>prophet</th>
      <th>RNN (tf)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2021-06-10</th>
      <td>7241</td>
      <td>7119</td>
      <td>8494</td>
    </tr>
    <tr>
      <th>2021-06-11</th>
      <td>7243</td>
      <td>7604</td>
      <td>8811</td>
    </tr>
    <tr>
      <th>2021-06-12</th>
      <td>7253</td>
      <td>7406</td>
      <td>8367</td>
    </tr>
    <tr>
      <th>2021-06-13</th>
      <td>7253</td>
      <td>7125</td>
      <td>7795</td>
    </tr>
    <tr>
      <th>2021-06-14</th>
      <td>7253</td>
      <td>6327</td>
      <td>7356</td>
    </tr>
    <tr>
      <th>2021-06-15</th>
      <td>7252</td>
      <td>5024</td>
      <td>6105</td>
    </tr>
    <tr>
      <th>2021-06-16</th>
      <td>7249</td>
      <td>5280</td>
      <td>6816</td>
    </tr>
  </tbody>
</table>
