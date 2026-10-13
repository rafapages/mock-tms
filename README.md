# Mock TMS: load data

Static mock load data for a HappyRobot demo (inbound carrier sales). Each file stands in for a load record in a broker's TMS. All data is fictional.

The voice agent's `find_load` tool fetches one load by ID:

```
GET <base-url>/loads/{load_id}.json
```

An unknown load ID returns 404, which the agent treats as "load not found".

| Load | Lane | Equipment | Status | Posted |
|---|---|---|---|---|
| 12345 | Chicago, IL → Dallas, TX | 53 ft dry van | available | $2,100 |
| 23456 | Atlanta, GA → Orlando, FL | 53 ft reefer | available | $1,150 |
| 34567 | Los Angeles, CA → Phoenix, AZ | 48 ft flatbed | available | $1,200 |
| 45678 | Memphis, TN → Indianapolis, IN | 53 ft dry van | covered | $1,250 |

The load records hold no negotiation ceiling. Pricing lives separately, standing in for the broker's pricing engine:

```
GET <base-url>/pricing/{load_id}.json
```

Each pricing file has the posted and maximum rate for a load. The agent's `evaluate_offer` tool reads it and applies the negotiation rules, so the agent itself never sees the maximum rate.

Pickup and delivery windows are relative ("Tomorrow, 8 AM to 12 PM") so the data never goes stale.
