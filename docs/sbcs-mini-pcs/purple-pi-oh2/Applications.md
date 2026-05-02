# Applications

<span class="badge badge-blue">Purple Pi OH2</span>&nbsp;
<span class="badge badge-blue">Docker</span>&nbsp;
<span class="badge badge-blue">Node-RED</span>&nbsp;
<span class="badge badge-orange">Home Assistant</span>

> This section focuses on learning essential tools such as Docker, Home Assistant, Node-RED, and OpenCV on the Purple Pi OH2. These technologies enable you to build, deploy, and manage smart applications ranging from IoT automation to computer vision systems. By setting up containerized environments, visual programming flows, home automation platforms, and image processing capabilities, the Purple Pi becomes a powerful edge computing device for real-world industrial and smart system applications.

---

## Docker Setup on Purple Pi OH2

### Overview

![Docker](images/docker-application.png)

Docker is a platform that allows you to run applications in lightweight containers. On the Purple Pi OH2, Docker helps you deploy and manage applications efficiently without worrying about system dependencies.

---

### Install Docker

**Update Package List**

```bash
sudo apt-get update
```

---

**Install Docker**

```bash
sudo apt install docker.io
```

---

**Verify Installation**

```bash
docker -v
```

You should see the installed Docker version.

---

### Configure Docker

**Edit Docker Daemon Configuration (Optional)**

```bash
sudo nano /etc/docker/daemon.json
```

---

**Restart Docker Service**

```bash
sudo systemctl restart docker
```

---

### Run Docker Without sudo

**Add User to Docker Group**

```bash
sudo usermod -aG docker $USER
```

**Apply Group Changes**

```bash
newgrp docker
```

---

### Re-login

* Exit all SSH sessions
* Close terminals
* Log out and log back in

---

### Test Docker Installation

**Run Test Container**

```bash
docker run hello-world
```

**Expected Output**

* Docker pulls the `hello-world` image
* A confirmation message is displayed

---

## Node-RED Installation

### Overview

![Nodered](images/nodered_banner.png)

Node-RED is a flow-based development tool for visual programming, widely used in IoT and industrial applications. On the Purple Pi OH2, it allows you to connect hardware devices, APIs, and online services using a browser-based editor.

---

### Install Node-RED (All-in-One Script)

The Node-RED team provides an official installation script that installs:

* Node.js
* Node-RED
* Required dependencies

**Run Installation Script**

```bash
bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
```

> This process may take some time depending on your internet speed.

---

![Nodered](images/install_node.png)

### Installation Prompts (Recommended Settings)

During installation, you will be asked several questions. Use the following answers:

* **Node-RED settings file initialization** → Press `Enter` (default)
* **Share anonymous usage information** → `No`
* **User security** → `No` *(can enable later)*
* **Projects feature** → `No`
* **Flow file** → `flows.json` (press `Enter`)
* **Encrypt credentials file** → Press `Enter` (skip)
* **Editor theme/style** → Default
* **Text editor component** → `Monaco`
* **Allow external modules in function nodes** → `Yes`

---

### Node-RED Control Commands

After installation, use the following commands to manage Node-RED:

Use `node-red-start` to start Node-RED

Use `node-red-stop` to stop Node-RED

Use `node-red-restart` to start Node-RED again

Use `node-red-log` to view the recent log output

Use `sudo systemctl enable nodered.service` to enable auto-start at boot

Use `sudo systemctl disable nodered.service` to disable auto-start at boot

---

### Access Node-RED Editor

**Open in Web Browser**

If you are using the Purple Pi locally:

```text
http://localhost:1880
```

If accessing from another computer on the same network:

```text
http://{Purple_Pi_OH2_IP_ADDRESS}:1880
```

> Replace `{Purple_Pi_OH2_IP_ADDRESS}` with your device IP (e.g., `192.168.1.100`)


![Interface](images/nodered.png)

