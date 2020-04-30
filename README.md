# Service link
https://minter-service.online/

# Template
```python
import pika

# user settings
login = ''
password = ''
host = ''
port = 0
q_name = ''


# function to handle incoming data
def callback(ch, method, properties, body):
    """
    Handles incoming data
    :param body: incoming data
    """
    print(body)


# setting amqp
url = f"amqp://{login}:{password}@{host}:{port}"
params = pika.URLParameters(url)
connection = pika.BlockingConnection(params)
channel = connection.channel()
channel.basic_consume(q_name, callback, auto_ack=True)

# start consuming
print(' [*] Waiting for messages:')
channel.start_consuming()
connection.close()

```