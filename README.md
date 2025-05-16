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

### Running RabbitMQ as Message Broker
![image](https://github.com/user-attachments/assets/e25b30ce-e1d2-4fb4-b1bc-7beb235b67ff)

### Sending and Processing Event
![image](https://github.com/user-attachments/assets/33dc39d0-8786-4de8-888a-50ec49cbdbdb)

Both the subscriber and publisher connect to the same RabbitMQ server using the AMQP URL `amqp://guest:guest@localhost:5672`.
The publisher sends a series of messages to the message broker, specifically to the `user_created` queue. Each message is a `UserCreatedEventMessage`, which contains a unique user ID and username.
The subscriber listens on the same `user_created` queue. When it receives a message, it processes and prints the content. In this example, it successfully receives and prints all 5 messages sent by the publisher.

After launching the subscriber with `cargo run`, we can check our RabbitMQ Management UI — and as seen on the tutorial, there should be at least one active connection, indicating that the subscriber is connected to the broker.
Then, when we run the publisher (`cargo run` in the publisher directory), it sends 5 events to RabbitMQ. These events are immediately consumed by the subscriber, which logs each message to the console.
