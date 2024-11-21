
# Minikube Setup on macOS

[Visit Reference](https://medium.com/@javatechie/kubernetes-tutorial-install-run-minikube-in-mac-os-k8s-cluster-369b25b0c3f0)

### Step 1: Check Virtualization Support
- **Check if Virtualization is Supported:**
  ```bash
  sysctl -a | grep -E --color 'machdep.cpu.features|VMX'
  ```

---

### Step 2: Install kubectl
- **Install kubectl using Homebrew:**
  ```bash
  brew install kubectl
  ```

- **Verify kubectl Version:**
  ```bash
  kubectl version
  ```

---

### Step 3: Install a Hypervisor
- **Options for Hypervisors:**
  - **HyperKit**
  - **VirtualBox**
  - **VMware Fusion**

- **Install HyperKit using Homebrew:**
  ```bash
  brew install hyperkit
  curl -LO https://github.com/kubernetes/minikube/releases/download/v1.34.0/minikube-darwin-arm64
  sudo install minikube-darwin-arm64 /usr/local/bin/minikube

  ```

- **Verify Installed Packages:**
  ```bash
  brew list
  ```

---

### Step 4: Install Minikube
- **Install Minikube using Homebrew:**
  ```bash
  brew install minikube
  ```

- **Check Minikube Version:**
  ```bash
  minikube version
  ```

---

### Step 5: Start Minikube
- **Start Minikube with Default HyperKit Driver:**
  ```bash
  minikube start

  minikube start --driver=docker
  ```

- **Check Minikube Status:**
  ```bash
  minikube status
  ```

---

### Step 6: Stop Minikube
- **Stop Your Minikube Cluster:**
  ```bash
  minikube stop
  ```

---

### Step 7: Delete Minikube
- **Delete Your Minikube Cluster:**
  ```bash
  minikube delete
  ```
