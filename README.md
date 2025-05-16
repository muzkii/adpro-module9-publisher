# Advanced Programming Rust 
by Andriyo Averill Fahrezi, NPM of 2306172325

## Module 9 - Software Architecture - Publisher

### Event-Driven Architecture – Publisher and AMQP Details

#### How much data does the publisher send to the message broker in one run?

The total amount of data the publisher sends to the message broker in one run depends on the number and size of the messages it publishes. For example, if the publisher sends **10 messages**, each with a payload of **100 bytes**, then the total data sent is:

```10 messages × 100 bytes = 1,000 bytes (or ~1 KB)```

In our current setup (based on the tutorial), the publisher sends a series of predefined messages (e.g., bus location updates).  
You can determine the exact data volume by logging or measuring the size of each message sent and counting the total number of messages during a run.

---

#### What does it mean if the URL `amqp://guest:guest@localhost:5672` is the same in both the subscriber and the publisher programs?

If both the **publisher** and **subscriber** use the same AMQP URL:

```amqp://guest:guest@localhost:5672```

It means:
- Both programs are connecting to the **same RabbitMQ broker** instance.
- The **publisher** sends messages to the broker.
- The **subscriber** receives messages from that broker.
- `guest:guest` — They both use the default username and password (`guest`) for authentication.
- `localhost:5672` — They both connect to a broker running locally on the default AMQP port `5672`.

This shared URL enables communication between the publisher and subscriber through the same messaging system, forming the core of the **event-driven architecture**.
