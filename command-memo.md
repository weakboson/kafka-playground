### Kafka Connect 設定

```shell
curl -X POST -H 'Content-Type:application/json' -d @config.json http://localhost:8082/connectors
```

### Console Producer / Consumer

```shell
kafka-console-producer --broker-list=localhost:19092 \
  --topic=connect-test \
  --property value.serializer=custom.class.serialization.JsonSerializer
```

```shell
kafka-console-consumer --bootstrap-server=localhost:19092 \
  --topic=connect-test \
  --property value.serializer=custom.class.serialization.JsonSerializer \
  --from-beginning
```

### Sink Connector が処理できるフォーマットについて

参考: https://rmoff.net/2017/09/06/kafka-connect-jsondeserializer-with-schemas.enable-requires-schema-and-payload-fields/

処理できないメッセージを発行してしまったときは以下のコマンドで削除。

```shell
kafka-topics --bootstrap-server=localhost:19092 --delete --topic=connect-test
```
