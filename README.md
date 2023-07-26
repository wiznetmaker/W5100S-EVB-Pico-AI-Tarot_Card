# W5100S-EVB-Pico-AI-Tarot_Card
W5100S-EVB-Pico + LCD + Button / Chat GPT + DALL-E2

## Choice! Check your fortune with tarot cards !
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/a4cfc166-05eb-4961-b509-d1b979c55e75)

![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/17d3ea0c-eada-4b4c-84df-79f1348b39d7)


### PROJECT DESCRIPTION
#### Intro
Hello! I made a fun project this time as well!

This project is very similar to the last one, but it's been upgraded a lot!

Check out the previous project for more information!

![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/27aa8408-6ac3-4325-b024-e8fad0058803)

Previous project

#### Hardware
The configuration is very simple! All you need is a W5100S capable of Ethernet communication with Raspberry pico. I used the W5100S-PoE board that I developed. And just configure the switch circuit to press the SPI-enabled LCD and switch like last time, and that's it!

![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/4df8cc3f-ede9-4deb-aef2-dd175f764068)

The pin setting is the same as the image above.

![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/f651f007-e52e-4667-b092-856900df56d7)

#### Ethernet Connectivity
The first thing to do is to do is to connect Ethernet. You can easily connect the Pico board to Ethernet by entering the Git below.

Getting Started
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/223dae96-c31e-47e8-8235-dc19daabf326)


You can configure the computer to be a server and the Pico to be a client.

#### Image transfer / Display
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/826aabfb-6c19-4173-846f-bffa375a070d)
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/997f8a27-bb8a-4a65-bfb9-0cf4e783fca0)

Pass the BMP image that has already been created over Ethernet. (Server)
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/b2d468e8-7f96-493e-bdfd-26b0b84b616c)

The client connects to the server and receives the image and displays it. (Client)

#### Select a card
You can choose the card you want with four buttons.
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/794a971c-cff1-4bda-99f3-52d01736cb4d)

In the Client, click the button for the desired card number. It calculates bits by bits and sends data to the server. When you click button 1, number 1 and 2 send 2, number 3 send 4, number 4 send 8.(Client)
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/7643ab60-b3f6-4768-83f9-36ba048ef7f9)

When the server receives the data, it converts the data into the desired characters. And make a string to deliver to GPT.(Server)

#### Chat GPT
You can easily get a Chat GPT API Key from the site below.
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/8e441aa1-7d51-41f0-a123-abab3ff89f6c)

![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/69e220c6-6c56-4662-8900-b799f7ff4423)

I assigned the following role to Chat GPT and wrote a prompt accordingly.(Server)
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/7a39a5f0-3e83-471f-afbc-af30ae5cb038)

The main code then combines the information about the click of a button received from the device into the prompt and forwards it to the GPT.(Server)

#### Dall-E-2
DALL-E 2 is an image generation tool created by OpenAI.
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/fc3de45d-cc27-4440-b17a-b09ebd93ad34)

The code for DALL-E 2 is structured as follows. One thing to note here is the Image size section. Since I don't have separate memory, I will save the image in BMP format to the Pico board's Flash and display it later.

Anyway, when sending and receiving data, the image size cannot be larger than the size of SRAM because the data is stored in SRAM.

In my experience, the program did not work properly when the image size exceeded 53k. I will upgrade this part in the future so that we can display even cooler images.
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/227c4ea1-98bb-4abd-aa47-e696db9e5e63)

In the main code, we send the data received from GPT back to DALL-E 2 as follows.

![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/fa2cca91-fdbb-4309-be43-144f1a54a891)

The Dall-E2 creates an image from the prompt sent by the GPT.
#### Display
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/ebbd15cb-37a8-4d09-9caa-f3a29fdae19a)

Send the data to the Client as you did in the process above to display the image created by the Dall-E2!
Card Description
#### Card Description
![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/87c1e3ea-1ad8-44fa-a584-170b853bce3f)
 
After displaying the image, send the string Card Description to the server. (Client)

![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/b11933c8-6e33-4281-8b4e-641e3a6cd3a5)

When the server receives the "Card Description" message, it sends the description of the card it received through the Chat GPT to the client again

![image](https://github.com/wiznetmaker/W5100S-EVB-Pico-AI-Tarot_Card/assets/111826791/53f65115-32eb-434a-b03d-f3fe57bc45a2)

The Client will display a description of the card.
#### Complete
https://youtu.be/63N3rUuBgTM

It's a motion video! Every morning, I use this tarot card to predict my luck.It's amazing that AI can do these things now!
