## Bad
```go
func NewRabbitConnection() RabbitConnection {
    r := RabbitConnection{}

    r.connection, err = amqp.Dial(url))
    if err != nil {
        logger.Log.WithFields(logrus.Fields{"context": "rabbit"}).Fatalf("%s: %s", "fehler 1, err)
    }

    r.Channel, err = r.connection.Channel()
    if err != nil {
        logger.Log.WithFields(logrus.Fields{"context": "rabbit"}).Fatalf("%s: %s", "fehler 2, err)
    }

    return r
}
```