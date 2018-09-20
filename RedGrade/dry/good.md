## Good
```go   
func NewRabbitConnection() RabbitConnection {
    r := RabbitConnection{}

    r.connection, err = amqp.Dial(url))
    r.FailOnError(err, "Fehler 1")

    r.Channel, err = r.connection.Channel()
    r.FailOnError(err, "Fehler 2")

}

func (r *RabbitConnection) FailOnError(err error, msg string) {
    if err != nil {
        logger.Log.WithFields(logrus.Fields{"context": "rabbit"}).Fatalf("%s: %s", msg, err)
    }
}
```