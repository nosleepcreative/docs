---
description: This page is incomplete
---

# Nexrender

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Built with love using nodejs • Brought to you by <a href="https://github.com/inlife">@inlife</a> and other <a href="https://github.com/inlife/nexrender/graphs/contributors">contributors</a></p></figcaption></figure>

## Abstract

This guide outlines the steps required to set up a nexrender rendering cluster, utilizing one EC2 instance as the nexrender server, your local machine as the worker node, and Google Sheets and Google Apps Script to send a curl request for a render job to the server.&#x20;

By following this configuration, users can easily establish a distributed rendering system for their projects, which can significantly reduce the time required for rendering complex tasks. The setup process is explained in detail, providing users with a clear understanding of the necessary components and how to connect them to create a functional rendering cluster.

{% hint style="info" %}
Overall, the client initiates requests to the server, the server manages the rendering process by assigning tasks to workers, and the API provides a programmatic interface for interacting with the server.
{% endhint %}

## Resources

* [https://www.npmjs.com/package/@nexrender/api](https://www.npmjs.com/package/@nexrender/api)
* [GitHub - inlife/nexrender: 📹 Data-driven render automation for After Effects](https://github.com/inlife/nexrender)
* [How to create an After Effects rendering bot](https://plainlyvideos.com/blog/after-effects-render-bot/)

## Checklist for rending cluster

1. Launch the cloud instances for the worker and server nodes
2. Ensure that the necessary files are accessible in Google Drive
3. Launch the worker node to initiate the rendering process
4. Set up the server node to receive and process rendering requests
5. Use a curl request to send a rendering job from the Google Sheets interface to the server node
6. Monitor the progress of the rendering job and retrieve the output files once completed

## Practice

Prior to setup your rendering cluster, you should familiarize yourself with sending a render job using your workstation to replace text and media (image, video, sound)

* [ ] Download the nexrender binaries from [Github](https://github.com/inlife/nexrender#using-binaries)
* [ ] Launch the CLI applications from the terminal
* [ ] Prepare an After Effects template. This should contain text or media to replace
* [ ] Prepare a JSON to send render bo

## How to set up a nexrender cluster

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

### Web Server & Environment Setup

To set up a server and install Nexrender on it, you can follow these general steps:

* [ ] **Choose a server -** You can use a cloud-based service like Amazon Web Services (AWS) or Microsoft Azure to set up a virtual server in the cloud, or you can use a physical server that you own or rent.
* [ ] **Choose an operating system** - Once you have your server, you'll need to choose an operating system to install on it. Nexrender supports Windows, macOS, and Linux, so you can choose the operating system that best suits your needs and preferences.
* [ ] **Download the nexrender binaries:** You can download the latest version of nexrender server and worker node from the official nexrender GitHub repository.

[Web Server Concepts and Examples](https://www.youtube.com/watch?v=9J1nJOivdyw)

[How to Create an EC2 Instance in AWS in 2023](https://youtu.be/0Gz-PUnEUF0)

### Modify Security Group

By default, most EC2 instances have their security group rules configured to block ICMP traffic. If this is the case, you will not be able to ping the IP address. You can try modifying the inbound rules of your instance's security group to allow ICMP traffic.&#x20;

Security Group: Edit Inbound rules - Custom TCP, Port Range: XXXX

#### Binary vs Programmatic Installation

if you just want to use Nexrender as a standalone tool to render After Effects projects, you can use the pre-built binary version. If you want to use Nexrender as a library in your own code or run the Nexrender Server on your own server, you should install the programmatic module via npm.

### Installation of Node.JS on EC2

The nexrender API can be installed and run on your EC2 instance as a Node.js application. The API can then be configured to listen for requests from your Google Form and trigger the rendering process on the nexrender server.

```javascript
sudo yum install -y gcc-c++ make
curl -sL https://rpm.nodesource.com/setup_16.x | sudo -E bash -
sudo yum install -y nodejss
```

### Installing nexrender server

[npm: @nexrender/server](https://www.npmjs.com/package/@nexrender/server)

#### Binary Installation

```jsx
wget <https://github.com/inlife/nexrender/releases/download/v1.43.0/nexrender-server-linux>
chmod +x nexrender-server-linux
./nexrender-server-linux
```

#### Launch ✅

```json
nexrender-server --port 3000 --secret=myapisecret
```

#### Installation

```json
npm install @nexrender/server --save

sudo npm install -g @nexrender/server
```

#### **Usage (programmatic)**

```jsx
const server = require('@nexrender/server')
const port = 3000
const secret = 'myapisecret'
server.listen(port, secret)
```

This code sets up a Nexrender server that will listen for incoming requests on port **`3000`** and require clients to provide a secret password in order to connect. Once the server is running, clients can connect to it and submit rendering jobs to be processed.

Here's how it works:

1. The first line of code imports the **`@nexrender/server`** package and assigns it to the **`server`** variable. This package provides the functionality to start a Nexrender server.
2. The second line of code sets the **`port`** variable to the value **`3000`**. This specifies the port on which the Nexrender server will listen for incoming connections.
3. The third line of code sets the **`secret`** variable to the value **`'myapisecret'`**. This is the API secret that clients will use to authenticate with the Nexrender server.
4. The fourth line of code starts the Nexrender server on the specified **`port`** and with the given **`secret`**. The **`server.listen()`** method is called with two arguments: the **`port`** and the **`secret`**. This method listens for incoming connections on the specified port and requires clients to provide the specified API secret when making requests to the server.

### Installing nexrender API

By using the [nexrender API](https://www.notion.so/duitbetter/Research-nexrender-cluster-91392910c0c6453695bebcef35d8bf9b?pvs=4#8721ca77d76e4c559fc8458459b9ffa0), you can automate the process of submitting jobs to nexrender, which can save you time and reduce the risk of errors. You can also use the API to retrieve job status and output files, which can be helpful for tracking job progress and managing rendered output.

#### Installation

```json
npm install @nexrender/api --save
```

#### Usage

```jsx
const { createClient } = require('@nexrender/api')

const client = createClient({
    host: '<http://3.15.46.159:3000>',
    secret: 'myapisecret',
    polling: 3000, // fetch udpates every 3000ms
})

const main = async () => {
    const result = await client.addJob({
        template: {
            src: 'file:///Users/ddu/Desktop/nexrender/project/project.aep',
            composition: 'main',
        }
    })

    result.on('created', job => console.log('project has been created'))
    result.on('started', job => console.log('project rendering started'))
    result.on('progress', (job, percents) => console.log('project is at: ' + percents + '%'))
    result.on('finished', job => console.log('project rendering finished'))
    result.on('error', err => console.log('project rendering error', err))
}

main().catch(console.error);
```

This code creates a client connection to a Nexrender API server, using the **`createClient`** method provided by the **`@nexrender/api`** package.

It then sets the host and secret credentials required to access the server, and sets the polling interval to check for job updates every 3000 milliseconds.

The **`main`** function uses the client to add a new job to the server, specifying the template source and composition to use. The **`result`** object is returned by the **`addJob`** method and is used to track the job's progress.

The **`result`** object also sets up event listeners to handle job events such as creation, starting, progress updates, completion, and errors. When an event is triggered, the corresponding callback function is called to handle it.

If you are running the Nexrender server on the same EC2 instance as the client script, you can use the internal IP address of the instance, which can be obtained by running the **`curl <http://169.254.169.254/latest/meta-data/local-ipv4`**> command from within the instance.

If you want to access the Nexrender server from outside the instance (for example, from your local computer), you would use the public IP address or DNS name of the EC2 instance, which you can find in the EC2 console or by running the **`curl <http://169.254.169.254/latest/meta-data/public-ipv4`**> command from within the instance. However, you would need to make sure that the necessary security group rules are in place to allow inbound traffic to the instance on the Nexrender server port.

**How to copy a file over**

```jsx
scp -i <path to private key> <local file path> <ec2-user>@<public IP or hostname>:<remote directory>
```

[Online API Testing Tool | Test Your API Online](https://reqbin.com/)

## nexrender-API



```json
mkdir nexrender-server
cd nexrender-server

npm init -y
**This will create a package.json file in the nexrender-server directory.**

**Run the following command to install the nexrender server node package:**
npm install nexrender-server
ls

Once the installation is complete, 
you can start the nexrender server node by running the following command:
nexrender-server
```

### Installing worker

Requirements: Windows/Mac

Pre-requisite: After Effects

If you have the binary file for the Nexrender Worker, you can still use it on your Mac laptop. To run the Nexrender Worker binary, you will need to open a terminal window and navigate to the directory where the binary file is located. Then, you can run the binary using the following command:

```
./nexrender-worker-macos
```

This will start the Nexrender Worker on your Mac laptop. By default, the worker will look for a Nexrender server running at **`http://localhost:3000`** and will not use a worker secret key.

#### Launch

If you need to connect the worker to a different server or use a worker secret key, you can pass command-line options to the binary. For example, to connect the worker to a server running at **`http://example.com:8080`** and use a worker secret key of **`abc123`**, you can run the following command:

```
./nexrender-worker-macos --host <http://18.191.217.227:3000> --secret myapisecret
```

[npm: @nexrender/worker](https://www.npmjs.com/package/@nexrender/worker)

[Deploy NodeJS APP on AWS EC2 Instance | NodeJS on EC2 | Running NodeJS APP on AWS EC2 | AWS Projects](https://www.youtube.com/watch?v=S45jZCvd2M8)

## Curl vs JavaScript API

Curl and JavaScript API client are both used for interacting with APIs, but they have different use cases and advantages.

**Curl** is a command-line tool used to transfer data to and from servers using various protocols, including HTTP, HTTPS, and FTP. It is useful for testing APIs or automating tasks that require interacting with servers through the command line. Curl is particularly useful for quick one-off requests or for scripting repetitive tasks.

On the other hand, a JavaScript API client, such as the @nexrender/api library shown in your example, is a software module that can be integrated into a web application to interact with an API. It is useful for more complex API interactions or when you need to handle API responses in a specific way.

The JavaScript API client provides a more user-friendly interface for interacting with the API, making it easier to handle responses and errors, and can be integrated into more complex applications. It also provides additional functionality, such as event listeners that can notify you of job progress or errors.

In summary, if you need to quickly test an API or automate tasks, curl is a good choice. If you are building a web application that interacts with an API, a JavaScript API client may be a better choice.

**Sending curl to server**

```jsx
curl \\
    --request POST \\
    --header "nexrender-secret: myapisecret" \\
    --header "content-type: application/json" \\
    --data '{"template":{"src": "file:///Users/ddu/Desktop/nexrender/project/project.aep",
            "composition": "MAIN"}}' \\
    <http://18.222.190.254:3000/api/v1/jobs>
```

## Submitting Form Responses to a server

#### Formatting Google Forms to JSON for nexrender

* **Set up a Google Form to collect render job details:** You can create a Google Form to collect details about the After Effects project to be rendered, such as the composition name, output format, and render settings.
* Create a script: You can use a programming language such as JavaScript, Python, or Ruby to create a script that reads the data from your Google Form and sends a request to the nexrender API.

