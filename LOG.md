Global API Key
```bash
# ccloud api-key create --resource "cloud"  # full environment
$ ccloud api-key create --resource lkc-z3rnd  #  Kafka cluster
+---------+------------------------------------------------------------------+
| API Key | IJUFE4GE4P2XKYKO                                                 |
| Secret  | T2Yo18Bh8q3qql3COadT5sVvAulKkeFTfD/ZEh6pPt8R2OPakqsFxToja9YzbBhT |
+---------+------------------------------------------------------------------+

$ ccloud api-key use --resource lkc-z3rnd IJUFE4GE4P2XKYKO
Set API Key "IJUFE4GE4P2XKYKO" as the active API key for "lkc-z3rnd".

# cluster name is like <project>-<api key type>-<provisioning method>
$ ccloud ksql app create ksqldb-client-iot-demo-global-cli --api-key IJUFE4GE4P2XKYKO --api-secret T2Yo18Bh8q3qql3COadT5sVvAulKkeFTfD/ZEh6pPt8R2OPakqsFxToja9YzbBhT --cluster lkc-z3rnd 
+--------------+--------------------------------------------------------+
| Id           | lksqlc-zzydd                                           |
| Name         | ksqldb-client-iot-demo-global-cli                      |
| Topic Prefix | pksqlc-9kn2y                                           |
| Kafka        | lkc-z3rnd                                              |
| Storage      |                                                    500 |
| Endpoint     | https://pksqlc-9kn2y.us-west-1.aws.confluent.cloud:443 |
| Status       | PROVISIONING                                           |
+--------------+--------------------------------------------------------+

$ ccloud api-key create --resource lksqlc-zzydd # for the KSQL cluster
+---------+------------------------------------------------------------------+
| API Key | QL3WK4G633I6HNRN                                                 |
| Secret  | 3+93ic19g4oAu5ibjusvsiUCJTbThG26FNFLKvr9LuP5a+qpRkIdu0RmNolroBnv |
+---------+------------------------------------------------------------------+

# $ ccloud ksql app configure-acls lksqlc-zzydd  users --cluster lkc-z3rnd
# Error: no service account found for KSQL cluster "lksqlc-zzydd"

curl -X "POST" "https://pksqlc-9kn2y.us-west-1.aws.confluent.cloud:443/ksql" \
     -H "Accept: application/vnd.ksql.v1+json" \
     --basic --user 'QL3WK4G633I6HNRN:3+93ic19g4oAu5ibjusvsiUCJTbThG26FNFLKvr9LuP5a+qpRkIdu0RmNolroBnv' \
     -d $'{
  "ksql": "LIST STREAMS;",
  "streamsProperties": {}
}'

```

Service Account API Key
```bash
Service account ksql-demo-jk already created.

$ ccloud api-key create \
    --resource lkc-z3rnd \
    --service-account $(ccloud service-account list | grep 'ksql-demo-jk ' | cut -f 3 -d " ") \
    --output human \
    --environment t36311
+---------+------------------------------------------------------------------+
| API Key | M5ODDF3YNWIUS5RE                                                 |
| Secret  | FjxyX3vk9ri77cjpL/JMjA7/jIgUO5GVaLRW/LVESLjGJbSgsrGuR1iAib2aj0PT |
+---------+------------------------------------------------------------------+

$ ccloud api-key use --resource lkc-z3rnd M5ODDF3YNWIUS5RE
Set API Key "M5ODDF3YNWIUS5RE" as the active API key for "lkc-z3rnd".


```