Deploy the app

```bash
az containerapp up -n $APP_NAME -g $RESOURCE_GROUP --environment $ENVIRONMENT --source .
```

Get the environment ID

```bash
ENVIRONMENT_ID=`az containerapp show -n $APP_NAME -g $RESOURCE_GROUP --query 'properties.managedEnvironmentId' -o tsv`
```

Get environment resource

```bash
az rest -m GET -u "$ENVIRONMENT_ID?api-version=2023-11-02-preview" -o jsonc
```

Modify the [config](env-enable-otel.json).

Enable otel

```bash
az rest -m PATCH -u "$ENVIRONMENT_ID?api-version=2023-11-02-preview" --body @env-enable.json
```

