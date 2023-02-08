# Writing A New Customer

Kafka producer publishes messages on a given topic. Kafka Consumer is a program, which consumes the published messages from the producer. The consumer consumes the message by subscribing to the topic. A single consumer can subscribe to multiple topics. Whenever the topic receives a new message it can process that message by calling defined functions. The following snippet is a sample of code which defines a class called TradeLicenseConsumer which contains a function called listen() which is subscribed to save-tl-tradelicense topic and calls a function to generate notification whenever any new message is received by the consumer.

{% code lineNumbers="true" %}
```
@Slf4j
@Component
public class TradeLicenseConsumer {

    private TLNotificationService notificationService;

    @Autowired
    public TradeLicenseConsumer(TLNotificationService notificationService) {
        this.notificationService = notificationService;
    }

    @KafkaListener(topics = {"save-tl-tradelicense")
    public void listen(final HashMap<String, Object> record, @Header(KafkaHeaders.RECEIVED_TOPIC) String topic) {
        notificationService.sendNotification(record);
    }
}
```
{% endcode %}

@KafkaListener annotation is used to create a consumer. Whenever any function has this annotation on it, it will act as kafka consumer and the message will go through the flow defined inside of this function. The topic name should be picked up from the application.properties file. This can be done as showed below:

```
@KafkaListener(topics = {"${persister.update.tradelicense.topic}")
```

where persister.update.tradelicense.topic is the key for the topic name in the application.properties

Whenever any new message is published on this topic the message will be consumed by the listen() function and will call the function sendNotification() with the message as the argument. The deserialization is controlled by the following two properties in the application.properties:

{% code lineNumbers="true" %}
```
spring.kafka.consumer.value-deserializer
spring.kafka.consumer.key-deserializer
```
{% endcode %}

The first property sets the deserializer for value while the second one sets it for the key. Depending on the deserializer we have set we can expect the argument in that format in our consumer function. For example, if we set the value deserializer to HashMapDeserializer and key deserializer to string like below:

```
spring.kafka.consumer.value-deserializer=org.egov.tracer.kafka.deserializer.HashMapDeserializer
spring.kafka.consumer.key-deserializer=org.apache.kafka.common.serialization.StringDeserializer
```

Then we can write our consumer function expecting HashMap as an argument like below:

```
public void listen(final HashMap<String, Object> record){...}
```

