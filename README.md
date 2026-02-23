Implementation Steps
1️⃣ Generate Private Key
openssl genrsa -out server.key 2048
2️⃣ Generate Self-Signed Certificate
openssl req -new -x509 -key server.key -out server.crt -days 365

Fill in the required certificate details.

3️⃣ Start TLS Server
openssl s_server -key server.key -cert server.crt -port 4433

The server will start listening on port 4433.

4️⃣ Connect Using TLS Client

Open a new terminal:

openssl s_client -connect localhost:4433

Packet Analysis

Open Wireshark

Apply filter:

tls

Observe:

ClientHello

ServerHello

Certificate Exchange

Encrypted Application Data
