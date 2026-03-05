TLS Server and Client Demonstration using OpenSSL

This project demonstrates how to create a simple TLS communication setup using OpenSSL.
It includes generating a private key, creating a self-signed certificate, running a TLS server, and connecting with a TLS client. Network packets are then analyzed using Wireshark.

Prerequisites

OpenSSL installed

Wireshark installed

Linux / Kali Linux / Ubuntu terminal

Check OpenSSL installation:

openssl version
Implementation Steps
1️⃣ Generate Private Key

Generate a 2048-bit RSA private key.

openssl genrsa -out server.key 2048

This creates a file:

server.key

which contains the server's private key.

2️⃣ Generate Self-Signed Certificate

Create a self-signed TLS certificate using the private key.

openssl req -new -x509 -key server.key -out server.crt -days 365

You will be asked to enter certificate details such as:

Country Name
State
Locality
Organization Name
Organizational Unit
Common Name
Email Address

This generates:

server.crt

which is the TLS certificate.

3️⃣ Start TLS Server

Run an OpenSSL TLS server using the generated key and certificate.

openssl s_server -key server.key -cert server.crt -port 4433

The server will now listen for secure TLS connections on:

localhost:4433
4️⃣ Connect Using TLS Client

Open another terminal and run:

openssl s_client -connect localhost:4433

This connects to the TLS server and establishes a secure connection.

You can now type messages between the client and server.

Packet Analysis using Wireshark

Open Wireshark

Start capturing on the loopback interface

Apply the filter:

tls
TLS Handshake Observed

During the connection, the following TLS handshake packets can be observed:

ClientHello
The client initiates the TLS handshake and sends supported cipher suites and TLS version.

ServerHello
The server responds with the selected cipher suite and TLS version.

Certificate Exchange
The server sends its self-signed certificate to the client.

Encrypted Application Data
After the handshake completes, communication becomes encrypted.

Files Generated
server.key   -> Private key
server.crt   -> Self-signed certificate
Tools Used

OpenSSL – TLS server and client

Wireshark – Network packet analysis

Kali Linux – Testing environment
