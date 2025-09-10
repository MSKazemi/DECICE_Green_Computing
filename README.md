# Carbon Intensity Forecasting API
This API provides endpoints to forecast carbon intensity using a pre-trained model for north Italy.
## Endpoints

- `/predictrange`: Forecast carbon intensity for a specified date range.
- `/predictday`: Forecast carbon intensity for the next 24 hours.
- `/predictweek`: Forecast carbon intensity for the next 7 days.
- `/predictmonth`: Forecast carbon intensity for the next 30 days.





```
docker build -t decicegreencomputing .
```


```
docker run -p 8000:8000 decicegreencomputing
```