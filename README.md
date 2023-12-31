<p align="center">
  <br>
  <img src="https://github.com/qvco/1secMail-Python/assets/77382767/fde69c1a-b95f-4d78-af1a-2dca315204bc" alt="1secMail" width="700">
<!--   <br>
  1secMail for Python
  <br> -->
</p>

<h4 align="center">An API wrapper for <a href="https://www.1secmail.com/" target="_blank">www.1secmail.com</a> written in Python.</h4>

  <p align="center">
    <img src="https://img.shields.io/github/release/qvco/1secMail-Python">
    <img src="https://img.shields.io/badge/python-3.8-blue.svg">
    <img src="https://img.shields.io/badge/License-MIT-blue.svg">
  </p>

### About

This is an easy to use yet full-featured Python API wrapper for www.1secmail.com ↗ using the official 1secMail API. It allows you to easily create temporary email addresses for testing, verification, or other purposes where you need a disposable email address.  
> Asynchronous operations are also supported!:thumbsup:

### Install

To install the package, you'll need Python 3.8 or above installed on your computer. From your command line:

```bash
pip install 1secMail
```

<br>

> **Note**
> If you're willing to install the development version, do the following:

```bash
git clone https://github.com/qvco/1secMail-Python.git

cd 1secMail-Python

pip install -r requirements.txt

pip install -e .
```

## Usage

### Generating Email Addresses

To generate a list of random email addresses, use the `random_email()` method:

```python
import secmail

client = secmail.Client()

client.random_email(amount=3)
>>> ['c3fho3cry1@1secmail.net', '5qcd3d36zr@1secmail.org', 'b6fgeothtg@1secmail.net']
```

You can also generate a custom email address by specifying the username and domain:

> **Note**
> Specifying a domain is optional!

```python
client.custom_email(username="bobby-bob", domain="kzccv.com")
>>> 'bobby-bob@kzccv.com'
```

### Receiving Messages

To wait until a new message is received, use the `await_new_message()` method:

```python
message = client.await_new_message("bobby-bob@kzccv.com")
```

To check all messages received on a particular email address, use the `get_inbox()` method and pass the email address:

```python
inbox = client.get_inbox("bobby-bob@kzccv.com")
for message in inbox:
    print(message.id)
    print(message.from_address)
    print(message.subject)
    print(message.date)
```

You can also fetch a single message using the `get_message()` method and passing the email address and message ID:

```python
message = client.get_message(address="bobby-bob@kzccv.com", message_id=235200687)
print(message.id)
print(message.subject)
print(message.body)
print(message.text_body)
print(message.html_body)
print(message.attachments)
print(message.date)
```

### Downloading an attachment

You can download an attachment from a message in the inbox of a specified email address using the download_attachment method like this:

```python
client.download_attachment(address, message_id, attachment_filename)
>>> 'Path: (C:\Users\user\path/config/rocket.png), Size: 49071B'
```

## Asynchronous Client

### Generating Email Addresses

To generate a list of random email addresses, use the `random_email()` method:

```python
import asyncio
import secmail

async def main():
    client = secmail.AsyncClient()
    email_addresses = await client.random_email(amount=3)
    print(email_addresses)

asyncio.run(main())
>>> ['c3fho3cry1@1secmail.net', '5qcd3d36zr@1secmail.org', 'b6fgeothtg@1secmail.net']
```

You can also generate a custom email address by specifying the username and domain:

> **Note**
> Specifying a domain is optional!

```python
await client.custom_email(username="bobby-bob", domain="kzccv.com")
>>> 'bobby-bob@kzccv.com'
```

### Receiving Messages

To wait until a new message is received, use the `await_new_message()` method:

```python
import asyncio
import secmail

async def main():
    client = secmail.AsyncClient()
    message = await client.await_new_message("bobby-bob@kzccv.com")
    print(f"{message.from_address}: {message.subject}")

asyncio.run(main())
```

To check all messages received on a particular email address, use the `get_inbox()` method and pass the email address:

```python
import asyncio
import secmail

async def main():
    client = secmail.AsyncClient()
    inbox = await client.get_inbox("bobby-bob@kzccv.com")
    print(f"You have {len(inbox)} messages in your inbox.")

    for message in inbox:
        print(message.id)
        print(message.from_address)
        print(message.subject)
        print(message.date)

asyncio.run(main())
```

You can also fetch a single message using the `get_message()` method and passing the email address and message ID:

```python
import asyncio
import secmail

async def main():
    client = secmail.AsyncClient()
    address = "bobby-bob@kzccv.com"
    inbox = await client.get_inbox(address)
    message_id = inbox[0].id
    message = await client.get_message(address, message_id)

    print(message.id)
    print(message.subject)
    print(message.body)
    print(message.text_body)
    print(message.html_body)
    print(message.attachments)
    print(message.date)

asyncio.run(main())
```

### Downloading an attachment

You can download an attachment from a message in the inbox of a specified email address using the download_attachment method like this:

```python
import asyncio
import secmail

async def main():
    client = secmail.AsyncClient()
    address = "bobby-bob@kzccv.com"
    inbox = await client.get_inbox(address)
    message_id = inbox[0].id
    message = await client.get_message(address, message_id)
    attachment_filename = message.attachments[0].filename
    await client.download_attachment(address, message_id, attachment_filename)

asyncio.run(main())

>>> 'Path: (C:\Users\user\path/config/rocket.png), Size: 49071B'
```

## Licnese

This software is licensed under the [MIT](https://github.com/qvco/1secMail-Python/blob/master/LICENSE) © [Qvco](https://github.com/qvco).
