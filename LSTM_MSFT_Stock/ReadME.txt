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


