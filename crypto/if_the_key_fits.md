Task:
I am trying to escape this 64-story horror house and the only way to escape is by finding the flag in this text file! Can you help me crack into the file and get the flag? The only hint I get is this random phrase: MWwwdjM1eW1tM3RyMWNrM3Q1ISEh

Steps:
1. If we look into the file, we can read `CREATED_BY\x00aescrypt (Windows GUI)`, this indicates the provided file was encrypted with `aescrypt`
2. I am too lazy to download aescrypt, so I am using the asesscript library in python instead
```python
!pip install pyAesCrypt

# The file encrypted as base64, so I can load it easily in Google Colab
import base64
b64 = "QUVTAgAAJkNSRUFURURfQlkAYWVzY3J5cHQgKFdpbmRvd3MgR1VJKSAzLjEwAIAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAfbvcn19wcNePjAXHD+7ExoKYirwZ/Vy4hZNQzZ34HWYjoNA4FH9GuAFjWmHy90YfFLB1GLH/sHrbDKXb8laBdvnvQ/y8qYAvUfdeYnAOjGl0OT8MDqLWBS/dWpw6J+jvdTHyD5QMZVho4fQyFhVn1CeNSorMejIg1Xd7AkQl2PTYSnsp72mpFEyoC2+hkGcFjzBCki0g2g2Q1TlNpIK1QAUDbOt6JuUkYQHDbhU/+vEmvDexoAjceq/SCWKHi288BQ=="
encoded_bytes = base64.b64decode(b64)

# Decrypt it
import pyAesCrypt
import io

bufferSize = 64 * 1024
password = bytes.decode(base64.b64decode("MWwwdjM1eW1tM3RyMWNrM3Q1ISEh"))

# input plaintext binary stream
fIn = io.BytesIO(encoded_bytes)

# initialize ciphertext binary stream
fDec = io.BytesIO()

# decrypt stream
pyAesCrypt.decryptStream(fIn, fDec, password, bufferSize)

# print decrypted data
print("Decrypted data:\n" + str(fDec.getvalue()))
```

The password to decode the file was provided within the task, but was base64 encoded. The output is:
`Congrats on finding the flag!\r\n\r\nNICC{1-4m-k3yn0ugh!}`, so the flag is `NICC{1-4m-k3yn0ugh!}`
