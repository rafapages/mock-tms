# Mock TMS: load data

Static mock load data for a HappyRobot demo (inbound carrier sales). Each file stands in for a load record in a broker's TMS. All data is fictional.

The voice agent's `find_load` tool fetches one load by ID:

```
GET <base-url>/loads/{load_id}.json
```

An unknown load ID returns 404, which the agent treats as "load not found".

| Load | Lane | Equipment | Status | Posted | Max |
|---|---|---|---|---|---|
| 12345 | Chicago, IL → Dallas, TX | 53 ft dry van | available | $2,100 | $2,350 |
| 23456 | Atlanta, GA → Orlando, FL | 53 ft reefer | available | $1,150 | $1,300 |
| 34567 | Los Angeles, CA → Phoenix, AZ | 48 ft flatbed | available | $1,200 | $1,350 |
| 45678 | Memphis, TN → Indianapolis, IN | 53 ft dry van | covered | $1,250 | $1,400 |

`max_rate_usd` is the negotiation ceiling. The agent uses it but never reveals it to the caller. In production this would come from the broker's pricing engine.

Pickup and delivery windows are relative ("Tomorrow, 8 AM to 12 PM") so the data never goes stale.
