To begin with, lets make an LSTM for predicting the MSFT stock price. Pick up data from yahoo finance

This model will be REALLY simple, only taking previous stock closing prices as inputs. 
Lets use a window size of 30 last days before prediction, predict the price for next day.
In every input there should be a date, could be have the date of our prediction day. 
So 30 stock prices and 1 date = 31 inputs into the LSTM, output is the stock price for target date


Overall this is pretty useless, as we use the actual predictions values in
the test data when the window moves (instead of adding the models own prediction),
the model then has the freedom to just be corrected whenever it is wrong, 
predicting 30 days ahead is more interesting I now realised.

KEY INSIGHT!
Dont try to predict the future price as the model will simply copy the actual data but be delayed, completely useless model which appear proper. Instead try to model the difference in Value from day to day, as that is not given away by previous data in the same way, meaning the model cannot cheat.

Random tip on further improvments for the Difference in value approach: 
"ive got a 6 gb csv file with the last 5000 days of price info for around 4800 companies merged with quarterly financial data like assets revenue etc merged with macro indicators like interest rates and all of that interpolated and cleaned up before passing to an lstm with many many layers with tuned hyper params. instead of using a standard loss value you should use mean absolute percentage error because if a stock is trading at 1$ and you have a loss of 1$ you would be off by 100% but if its trading at 1000$ and yoru loss is 10 then you would be off by 1%.

also try to use time distributed lstm layers at the input and to use leaky relu not just relu so that parts of the model that arnt use often dont just become dead weight . Also use a deeper model to capture the complex relationship between the columns in the training data and MOST IMPORTANTLY..... Kill any over fitting with lots of dropout layers and batch norm"

