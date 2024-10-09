** Steps:

*Data Preprocessing:
1.Load stock price data from a CSV file.
2.Handle missing values, non-numeric columns (Change % and Volume), and convert them into appropriate formats.
3.Add common technical indicators: 10-day and 50-day moving averages (MA10, MA50), exponential moving average (EMA10), RSI, and MACD.

*Exploratory Data Analysis:
1.Visualize stock prices over time, distribution of closing prices, and changes in percentage.
2.Use rolling means and standard deviations to check for trends.
3.Use a lag plot and autocorrelation to evaluate the time series nature of the data.

*Data Scaling:
1.Use MinMaxScaler to normalize the features and target (Close prices) to a range between 0 and 1.
2.The normalization ensures that the features have the same scale, which is important for LSTM models.

*Sequence Creation:
1.Prepare the data in sequences for the LSTM model by creating time steps (look-back periods).
2.Here, 60 time steps are used, meaning each training sample contains 60 consecutive days of stock data.

*LSTM Model:
1.The model is built using a Bidirectional LSTM layer followed by a regular LSTM layer. Both layers include dropout to prevent overfitting.
2.Dense layers are used to refine the predictions, and the model outputs a single value: the predicted closing price.
3.The Adam optimizer is used with a learning rate of 0.001, and the loss function is mean absolute error (MAE).

Model Training:

The model is trained using the training set, and the test set is used for validation.
Early stopping, model checkpointing, and learning rate scheduling are applied as callbacks to optimize the training process.
The training continues for a maximum of 50 epochs, but it can stop earlier if validation loss does not improve for 10 consecutive epochs (patience).
Predictions:

Once the model is trained, it predicts the stock prices on the test set.
The predictions are scaled back to the original range using the inverse transformation of MinMaxScaler.
Performance Evaluation:

The model's performance is evaluated by calculating the mean absolute error (MAE) between the predicted and actual stock prices.
