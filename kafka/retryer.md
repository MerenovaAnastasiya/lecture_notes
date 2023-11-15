KafkaMessageListenerContainer - читает из всех топиков в один поток
![img.png](img.png)
ConcurrentMessageListenerContainer - содержит в себе List<KafkaMessageListenerContainer<K, V>> делегирует им обработку сообщений в многопоточном режиме

обратить внимание на RecordInterceptor и BatchInterceptor!


