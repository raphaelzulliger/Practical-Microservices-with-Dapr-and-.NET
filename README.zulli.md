# What I've done

## Switch to MongoDB (self-hosted)

I replaced Azure CosmosDB to a local, self-hosted MongoDB instance.

```sh
docker run --name mydapr_state-mongo --restart=always -p 27017:27017 -d mongo
```

Run the shipping service:

```sh
dapr run --app-id "shipping-service" --app-port "5005" --dapr-grpc-port "50050" --dapr-http-port "5050" --components-path "./components-self-hosted" -- dotnet run --project ./sample.microservice.shipping/sample.microservice.shipping.csproj --urls="http://+:5005"
```

publish:

```sh
dapr publish --publish-app-id "shipping-service" --pubsub commonpubsub -t OnOrder_Prepared -d '"{\"OrderId\": \"08ec11cc-7591-4702-bb4d-7e86787b64fe\"}"'
```
