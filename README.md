# 🐳 Docker Volumes Practical – Named, Bind & Anonymous

> Hands-on implementation of Docker storage mechanisms to understand persistent data in containers.

---

## 📌 Project Objective

This project demonstrates practical implementation of all three Docker volume types:

- 🔹 Named Volume  
- 🔹 Bind Mount  
- 🔹 Anonymous Volume  

The goal is to understand how Docker handles persistent storage and how data survives beyond container lifecycle.

---

# 🏗️ Architecture Diagram

![Docker Volume Architecture](/img/Docker-volume_diagram.png)

---

# 📦 Understanding Docker Storage

By default, containers are **ephemeral**.  
If a container is removed, its internal data is lost.

Docker Volumes solve this problem by storing data outside the container layer.

---

# 🔷 1️⃣ Named Volume (Recommended for Production)

## Step 1: Create Volume

```bash
docker volume create myvolume
```

## Step 2: Verify Volume
```
docker volume ls
```
### 📸 Screenshot:
**![](/img/Screenshot%20(1111).png)**

## Step 3: Run Container with Named Volume
```
docker run -it --name named-test -v myvolume:/data alpine
```

## Inside container:
```
cd /data
touch file1.txt
exit
```
## Remove container:
```
docker rm named-test
```

## Run again:
```
docker run -it --name named-test2 -v myvolume:/data alpine
cd /data
ls
```
### 📸 Screenshot:
**![](/img/Screenshot%20(1112).png)**
**![](/img/Screenshot%20(1113).png)**
**![](/img/Screenshot%20(1114).png)**

# 🔷 2️⃣ Bind Mount (Host Directory Mapping)

## Step 1: Create Host Directory
```
mkdir hostdata
```

## Step 2: Run Container
```
docker run -it --name bind-test -v $(pwd)/hostdata:/data alpine
```

## Inside container:
```
cd /data
touch bindfile.txt
exit
```

## Step 3: Verify on Host
```
ls hostdata
```
### 📸 Screenshot:
**![](/img/Screenshot%20(1115).png)**
**![](/img/Screenshot%20(1116).png)**

# 🔷 3️⃣ Anonymous Volume

## Run Container
```
docker run -it --name anon-test -v /data alpine
```

## Inside container:
```
cd /data
touch anonfile.txt
exit
```

## Check Volumes
```
docker volume ls
```

### 📸 Screenshot:
**![](/img/Screenshot%20(1117).png)**
---

--
| Feature          | Named Volume | Bind Mount | Anonymous   |
| ---------------- | ------------ | ---------- | ----------- |
| Managed By       | Docker       | Host       | Docker      |
| Persistent       | ✅ Yes        | ✅ Yes      | ✅ Yes       |
| Easy to Manage   | ✅ Yes        | ⚠️ Medium  | ❌ No        |
| Production Ready | ✅ Yes        | Dev/Test   | ❌ Not Ideal |

---

## 🎯 Key Learning Outcomes

- Containers are ephemeral by default

- Docker volumes persist data beyond container lifecycle

- Named volumes are best for databases

- Bind mounts are useful for development

- Anonymous volumes are auto-generated and less manageable

---


## 🛠️ Commands Used
```
docker volume create
docker volume ls
docker volume inspect
docker run -v
docker rm
```
## 🚀 Author

### Vivek Chopade

- DevOps Learner
- Docker | AWS | Terraform | Ansible | Docker | 
