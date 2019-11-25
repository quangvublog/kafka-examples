# Kafka with Python

A collection of Kafka example use Python.

## Requirements

- Virtualenv
- Python 3
- Confluent Kafka

**Setup Python Environtment**

```
$ cd kafka-python
$ virtualenv -p python3 venv
$ source venv/bin/activate
$ pip install -r requirements.txt
```

**Test it**

Be sure you start Apache Kafka server already.

```
$ python consume_example.py
$ python produce_example.py
```

