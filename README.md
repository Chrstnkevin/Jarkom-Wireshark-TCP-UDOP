# Jarkom-Wireshark-TCP-UDOP

| Nama   | NRP  |
|-----------|-----------|
| Christian Kevin Emor | 5025211153 |

# Materi 4 : TCP
### Soal No 1
> What is the IP address and TCP port number used by the client computer (source) that is transferring the alice.txt file to gaia.cs.umass.edu? To answer this question, it’s probably easiest to select an HTTP message and explore the details of the TCP packet used to carry this HTTP message, using the “details of the selected packet header window” (refer to Figure 2 in the “Getting Started with Wireshark” Lab if you’re uncertain about the Wireshark windows).

Klik pada filtering dan masukkan
````
http
````
maka akan muncul hasil berikut dan tekan Transmission Control Protocol lalu didapatkan seperti berikut
````
Ip Address : 192.168.86.68
Port       : 55639
````
![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/75a88dd2-d3d8-45a1-b152-65c1c910e1c2)

### Soal No 2
> What is the IP address of gaia.cs.umass.edu? On what port number is it sending and receiving TCP segments for this connection?

Pada soal no 1 telah dilakukan filtering dan kita bisa melihat IP Address dari gaia.cs.umass.edu adalah
````
IP Address : 128.119.245.12
Port       : 80
````
![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/10a59a9c-2a59-4f70-87a2-cedf6ef2d30a)

### Soal No 3
> What is the sequence number of the TCP SYN segment that is used to initiate the TCP connection between the client computer and gaia.cs.umass.edu? (Note: this is the “raw” sequence number carried in the TCP segment itself; it is NOT the packet # in the “No.” column in the Wireshark window. Remember there is no such thing as a “packet number” in TCP or UDP; as you know, there are sequence numbers in TCP and that’s what we’re after here. Also note that this is not the relative sequence number with respect to the starting sequence number of this TCP session.). What is it in this TCP segment that identifies the segment as a SYN segment? Will the TCP receiver in this session be able to use Selective Acknowledgments (allowing TCP to function a bit more like a “selective repeat” receiver, see section 3.4.5 in the text)?

masukkan pada filetring
````
tcp
````
dan didapatkan hasil sebagai berikut, lalu pilih yang ada SYN maka bisa didapatkan sequence numbernya
````
TCP SYN sequence number (raw) : 4236649187
Flag 0x002 identifies the segment as SYN
Certainly, the recipient is able to utilize Selective Acknowledgements since the packet allows for SACK.
````
![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/87ecdf43-86ea-406a-9dd0-59b195a8dc6d)

### Soal No 4
> What is the sequence number of the SYNACK segment sent by gaia.cs.umass.edu to the client computer in reply to the SYN? What is it in the segment that identifies the segment as a SYNACK segment? What is the value of the Acknowledgement field in the SYNACK segment? How did gaia.cs.umass.edu determine that value?

Seperti No 3 akan tetapi pilih SYN, ACK dan didapatkan hasil
````
Sequence number : 1068969752
Flag            : 0x012
ACK value       : 4236649187
````

![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/a824b2f0-7990-4fd4-9e9e-9cb6c0edf274)

### Soal No 5
> What is the sequence number of the TCP segment containing the header of the HTTP POST command? Note that in order to find the POST message header, you’ll need to dig into the packet content field at the bottom of the Wireshark window, looking for a segment with the ASCII text “POST” within its DATA field. How many bytes of data are contained in the payload (data) field of this TCP segment? Did all of the data in the transferred file alice.txt fit into this single segment?

Pilih SYN lalu didapatkan hasil bahwa
````
Sequence number : 4236649188
Payload         : 1514 bytes
No.
````
![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/6ecf742b-6dab-40d7-99ca-a622cf4a5c1b)

### Soal No 6
> Consider the TCP segment containing the HTTP “POST” as the first segment in the data transfer part of the TCP connection.

masukkan filter
````
http.request.method == "POST"
````
didapatkan bahwa 
> - At what time was the first segment (the one containing the HTTP POST) in the data-transfer part of the TCP connection sent?

data tiba pada
````
Arrival Time: Feb  3, 2021 09:43:26.840557000 SE Asia Standard Time
````
![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/bc8e5083-e33b-4a20-b93e-ea2e376aeca2)

> - At what time was the ACK for this first data-containing segment received?

lihat packet responnya dan data diterima pada
````
Arrival Time: Feb  3, 2021 09:43:26.885500000 SE Asia Standard Time
````
![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/d1911104-d3a0-40bb-a3d8-429bb1c7beaf)

> - What is the EstimatedRTT value (see Section 3.5.3, in the text) after the ACK for the second data-carrying segment is received? Assume that in making this calculation after the received of the ACK for the second segment, that the initial value of EstimatedRTT is equal to the measured RTT for the first segment, and then is computed using the EstimatedRTT equation on page 242, and a value of alpha = 0.125.
> _Note: Wireshark has a nice feature that allows you to plot the RTT for each of the TCP segments sent. Select a TCP segment in the “listing of captured packets” window that is being sent from the client to the gaia.cs.umass.edu server. Then select: Statistics->TCP Stream Graph-Round Trip Time Graph._

dari dua informasi diatas bisa didapatkan bahwa RTT atau Round Trip Time dari data yang di POST adalah **0.044942443 s**

### Soal No 7
> What is the length (header plus payload) of each of the first four data-carrying TCP segments?

**Fisrt Frame Length 7**
````
Frame 153: **1451 bytes** on wire (11608 bits), 1451 bytes captured (11608 bits) on interface en0, id 0
````
![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/75c8881c-5a67-4c90-9325-f2e1b4269b09)

**Second Frame Length 7**
````
Frame 179: **843 bytes** on wire (6744 bits), 843 bytes captured (6744 bits) on interface en0, id 0
````
![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/578a85d4-7252-47d0-b975-09335069bd0d)

# Materi 5 : UDP
### Soal No 1
> Select the first UDP segment in your trace. What is the packet number4 of this segment in the trace file? What type of application-layer payload or protocol message is being carried in this UDP segment? Look at the details of this packet in Wireshark. How many fields there are in the UDP header? (You shouldn’t look in the textbook! Answer these questions directly from what you observe in the packet trace.) What are the names of these fields?

````
1. Packet 5
2. SSDP
3. Dari packet di bawah, didapatkan bahwa terdapat 4 field pada UDP header yaitu Source Port, Destination Port, Length, dan Checksum.
````
![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/60f396e0-270a-4c1a-946a-7cb895f940e0)

### Soal No 2
> By consulting the displayed information in Wireshark’s packet content field for this packet (or by consulting the textbook), what is the length (in bytes) of each of the UDP header fields?

````
total length dari UDP header adalah 2 + 2 + 2 + 2 = 8 bytes
````
![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/9eff0874-c652-4de1-b7f2-23295e17709a)

### Soal No 3
> The value in the Length field is the length of what? (You can consult the text for this answer). Verify your claim with your captured UDP packet. 

````
Length: 283
````
![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/852f68f5-6f6e-4ce1-b92f-8d62f18f9205)

### Soal No 4
> What is the maximum number of bytes that can be included in a UDP payload? (Hint: the answer to this question can be determined by your answer to 2. above)

Maksimum jumlah byte yang dapat dimuat dalam payload UDP adalah 65.527 byte. UDP memiliki bidang 16-bit untuk panjang payload, yang mampu mewakili angka dari 0 hingga 65.535 (2^16 - 1). Namun, header UDP memiliki panjang 8 byte. Dengan demikian, ukuran payload terbesar adalah 65.535 - 8 = 65.527 byte. Ini mewakili jumlah data maksimum yang dapat diangkut oleh payload sebuah paket UDP tunggal.

### Soal No 5
> What is the largest possible source port number? (Hint: see the hint in 4.)

Nomor port sumber tertinggi yang dapat digunakan dalam konteks protokol lapisan transportasi UDP atau TCP adalah 65.535. Ini disebabkan oleh penggunaan representasi 16 bit, yang memungkinkan angka dari 0 hingga 65.535 (2^16 - 1). Nomor port digunakan untuk mengenali berbagai titik akhir komunikasi di dalam sebuah host, dan mereka merupakan bagian penting dari sistem addressing dalam komunikasi jaringan.

### Soal No 6
> What is the protocol number for UDP? Give your answer in decimal notation. To answer this question, you’ll need to look into the Protocol field of the IP datagram containing this UDP segment (see Figure 4.13 in the text, and the discussion of IP header fields).

didapatkan hasil : 17

![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/b411488b-c378-4022-9eb6-7c0012349b69)

### Soal No 7
> Examine the pair of UDP packets in which your host sends the first UDP packet and the second UDP packet is a reply to this first UDP packet. (Hint: for a second packet to be sent in response to a first packet, the sender of the first packet should be the destination of the second packet).
> What is the packet number5 of the first of these two UDP segments in the trace file?

First packet is 15

> What is the packet number6 of the second of these two UDP segments in the trace file?

Second packet is 17
![image](https://github.com/Chrstnkevin/Jarkom-Wireshark-TCP-UDP/assets/97864068/8c776e98-6018-4c74-9531-41591f2d70d4)

> Describe the relationship between the port numbers in the two packets.

The destination port number in packet 15 (the request) corresponds to the source port number in packet 17 (the reply), and vice versa.
