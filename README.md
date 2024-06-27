# Ollama On AWS

This repo is a companion to the YouTube video titled: [UNLEASHING the Power of Ollama + Llama 3 in the Cloud](https://youtu.be/rr-cEvLcOWw). It includes all commands used in the video.

### Be sure to shutdown your EC2 instance when you are no longer using it to avoid unneeded cost!

## Sign Up for AWS Account

[Create AWS Account](https://signin.aws.amazon.com/signup?request_type=register)

## EC2 Instance User Data

Copy the commands below and paste them in the User Data section when setting up your EC2 instance.

```bash
#!/bin/bash
curl -fsSL https://ollama.com/install.sh | sh
sudo systemctl start ollama
```

## Ollama Install

[Ollama Linux install link](https://ollama.com/download/linux)

## SSH into Ollama Server

Use the commands below to ssh into your Ollama server.

### Change ssh key permissions

```
sudo chmod 600 <your-ssh-key-name.pem>
```

```
sudo chmod 600 ollama-key.pem
```

### SSH into Ollama Server

```
ssh -i <your-ssh-key-name.pem> ubuntu@<public_ip_address_assigned_to_your_ec2>
```

#### Example

```
ssh -i ollama-key.pem ubuntu@137.23.12.94
```

## Enable Ollama to run as dedicated server

Step 1

```
sudo systemctl edit ollama.service
```

Step 2

Paste the below configuration into the ollama.service file

```
[Service]
Environment="OLLAMA_HOST=0.0.0.0"
```

Step 3

Run the below command

```
sudo systemctl restart ollama
```

Step 4

Check the status of the Ollama server

```
sudo systemctl status ollama
```

## Ollama Commands

### Available Ollama Models

[Ollama Models](https://ollama.com/library)

### List Ollama Models

```
ollama list
```

### Pull Ollama Model

```
ollama pull <ollama_model_name>
```

```
ollama pull llama3
```

### Run Ollama Model

```
ollama run <ollama_model_name>
```

```
ollama run llama3
```

## Testing Ollama API

### Streaming output test

```
curl http://54.145.158.114:11434/api/generate -d '{
	  "model": "llama3",
	  "prompt": "write simple java code to divide two numbers",
	  "stream": true
	}'
```

### Non Streaming output test

```
curl http://54.145.158.114:11434/api/generate -d '{
	  "model": "llama3",
	  "prompt": "write simple java code to divide two numbers",
	  "stream": false
	}'
```

### Be sure to shutdown your EC2 instance when you are no longer using it to avoid unneeded cost!
