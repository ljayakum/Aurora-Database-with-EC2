# Aurora-Database-with-EC2

Aurora is a **relational database** service by **AWS**.  
In this project, we'll set up **Amazon Aurora** to store data and connect it to an **EC2 instance**.

> ⚠️ The web app will come in the next project — this one focuses on database setup and connection.
>
> ## 🔹 What is Aurora?
- AWS-managed **relational database**
- Compatible with MySQL & PostgreSQL
- Scalable, high-performance, and secure

## 🔹 Why Use Aurora?
- Store, update, and retrieve data
- Reliable backend for web apps

## 🔹 Project Goal
- Create Aurora DB
- Launch EC2 instance (web server)
- Connect EC2 to Aurora securely

The architecure diagram for today's project

- ![architecture](https://github.com/user-attachments/assets/c949a0dd-410e-4146-bc6b-9b2e08243f94)

## ✅ Step 1: Use Your IAM User (Not Root)

For this project, make sure you're using your **IAM user**, not the **root user**.

> 🔐 AWS recommends **not using the root user** for daily tasks to reduce the risk of security breaches. — We’ll skip the setup here and jump straight to Step 2!
>
> ![iam login](https://github.com/user-attachments/assets/203229d7-9912-4e87-b714-8c7f7ac0ff64)

## ✅ Step 2: Understand Relational Databases

> ⚡ **Aurora is a great choice** when your project requires **high performance** and **high availability** for large-scale relational databases.

A **relational database** organizes data in **rows and columns**, similar to spreadsheets or tables.

> 🗃️ Amazon RDS (Relational Database Service) is used to create and manage these structured databases in the cloud.

> 🌍 **Tip:** Before creating your database, choose the **right AWS region** for your project.  
> Selecting a region close to your users or EC2 instance helps reduce **latency** and improves performance.

Create an Aurora Database

1. In the **left navigation bar**, click **Databases**.
2. Under the **Databases** section, select **Create database**.
3. On the **Create database** page, choose **Standard Create**.
4. In the **Configuration** section:
   - For **Engine type**, select **Aurora (MySQL-Compatible)**.
   - ![right rds](https://github.com/user-attachments/assets/7bd90470-86fe-4b0a-b654-09b998cab2b9)
  
   - In the **Settings** section:

- **DB cluster identifier:** `nextwork-db-cluster`
- **Master username:** `admin`
- **Credentials management:** Select **Self managed**
- **Master password:** Choose a secure password (e.g., `n3xtw0rk`)
- **Confirm password:** Re-type the password

> 🔐 **Important:** Save your database login credentials — 

Leave **Cluster storage configuration** settings as **default**.

In the **Instance configuration** section:

> 💡 **Burstable classes** like `t3.medium` offer a cost-effective way to handle variable workloads with baseline CPU and burst capability.

 ![ec2](https://github.com/user-attachments/assets/b8e31495-cf28-433f-b908-0bfabeeecd62)

- **Instance class type:** Choose **Burstable classes (includes t classes)**
- **Instance size:** Select `db.t3.medium`

> ⏸️ I am pausing the Aurora setup here because it needs to connect to an **EC2 instance**.  
> Let’s set up the EC2 instance first before completing the database configuration.
>
> ## ✅ Step 3: Launch Your EC2 Instance (Web Server)
>
> 🖥️ Next, I will **launch an EC2 instance**, which will act as the **web server** hosting our future web application.

1. In the **left-hand menu**, select **Instances** and click **Launch instances**.

2. On the **Launch an instance** page, configure the following:

   - **Name and tags**:  
     - **Name**: `nextwork-ec2-instance-web-server`
     
   - **Application and OS Images (AMI)**:  
     - Choose **Amazon Linux**  
     - Select **Amazon Linux 2023 AMI**

     ![ec2 instances t2 micro](https://github.com/user-attachments/assets/165d0d68-2817-4002-ac71-423bbb9d7845)


4. Keep the **default settings** for the rest of the options.

> ✅ I created a **new key pair** for my EC2 instance. This key helps **secure the instance** and gives me **direct SSH access**.  
> With this access, I’ll be able to **configure the server**, build the **web app**, and **connect it to the Aurora database**.


>### 🔑 Key Pair Settings

- **Key pair name**: `NextWorkAuroraApp`
- **Key pair type**: Leave as **RSA**
- **Private key file format**: Leave as **.pem**

![Key pair](https://github.com/user-attachments/assets/996a4566-1d3f-4bae-873e-f9d9abf4016d)

> 🗝️ The key pair lets you securely access your EC2 instance using SSH.  
> You'll need this key to log in, make updates, or manage your server later.
>
> ## ✅ Step 4: Review Summary & Launch EC2 Instance

Before launching, review the **Summary panel**. Here's what it tells you:

- 💻 **Number of instances** – How many virtual machines you're launching.
- 🎨 **Software Image (AMI)** – The OS your instance will run (e.g., Amazon Linux 2023).
- ⚙️ **Virtual server type** – Instance type (CPU, memory, network performance).
- 👮 **Firewall** – EC2 uses **Security Groups** to control inbound/outbound traffic.
- 🪣 **Storage** – Disk storage for your instance.

> Finally, click **Launch instance**.

![ec2 with details](https://github.com/user-attachments/assets/a4f743d5-ac73-4eec-96fd-74c1a1e5528e)

### 🔍 After Launch: Check Key Details

> 📝 We just created an EC2 instance and took note of two key details:
> 
> - **Public IPv4 DNS** – Tells us **where** our EC2 instance (web server) is located.
> - **Key pair name** – Allows us to **securely access** the instance via SSH.
> 
> Together, these details let us connect to and configure our EC2 web server.

1. Go back to the **EC2 Instances list**.
2. Select the checkbox next to your newly created instance.
3. Under the **Details** tab, note:
   - **Public IPv4 DNS** – Used to connect to your EC2 via SSH or browser.
   - **Key pair name** – Confirms the key you’ll use for secure access.

Finish Creating Your Aurora Database

1. In the **Compute resource** section, select **Connect to an EC2 compute resource**.
2. From the **EC2 instance** drop-down, choose:  
   `nextwork-ec2-instance-web-server`

![aurora ec2 instances](https://github.com/user-attachments/assets/f1f28fe1-61fa-4c44-acdb-90dcf7669dfc)

> 🔄 **Note:** If your EC2 instance doesn't show up right away, click the **refresh** button next to the drop-down menu.

> ✅ Finally, leave the remaining settings at their **default values** and click **Create database**.
![aurora configuration](https://github.com/user-attachments/assets/b4b8de05-fd3f-4aaf-89a5-f238e17042ec)

![fianlly create data base](https://github.com/user-attachments/assets/b43f462c-24c2-48a4-9b72-1c597d06087d)

> ⚠️ **Reminder:** I plan to **delete the resources** after testing to avoid any additional AWS charges.
![creating db](https://github.com/user-attachments/assets/e87b6a28-9576-4e8c-bf94-82aa32d3aecd)

## 🔄 What is a Database Cluster in Aurora?

Aurora uses **database clusters** to deliver high performance and availability — perfect for big workloads.

- A **cluster** is a group of database instances working together.
- It includes:
  - A **primary instance** for all write operations
  - One or more **read replicas** for backups and read scaling
- If the primary fails, a **replica is automatically promoted**, ensuring minimal downtime.

> 🔧 This setup makes Aurora **fault-tolerant**, **scalable**, and **highly available**.
>
> Aurora uses **database clusters** to ensure **high availability**.  
Clusters work by maintaining **multiple copies** of your data.

> ## 🏁 Final Notes & Key Takeaways

- 🔐 **Use IAM users**, not root, for secure AWS operations.
- 🌐 **Choose the right AWS region** to reduce latency and improve performance.
- 💾 **Aurora is a relational database** designed for high performance and scalability.
- 🛠️ Aurora uses **clusters** with a primary instance and read replicas to ensure **high availability**.
- 🖥️ Launch an **EC2 instance** to act as your **web server**, which will connect to the Aurora DB.
- 🔑 **Key pairs** are required for secure SSH access to EC2. Store your `.pem` file safely.
- 🌍 Save your EC2’s **Public IPv4 DNS** — it's your way in!
- 🧹 **Delete resources** after use to **avoid unexpected AWS charges**.

> ✅ With Aurora and EC2 set up, you're ready to build and connect your web application in the next project!

If the **primary instance** fails, one of the **read replicas** takes over, so your database remains available and operational.
![final created](https://github.com/user-attachments/assets/c6fb7072-c19d-435b-9e8c-e12db302325f)

> ## 🏁 Final Notes & Key Takeaways

- 🔐 **Use IAM users**, not root, for secure AWS operations.
- 🌐 **Choose the right AWS region** to reduce latency and improve performance.
- 💾 **Aurora is a relational database** designed for high performance and scalability.
- 🛠️ Aurora uses **clusters** with a primary instance and read replicas to ensure **high availability**.
- 🖥️ Launch an **EC2 instance** to act as your **web server**, which will connect to the Aurora DB.
- 🔑 **Key pairs** are required for secure SSH access to EC2. Store your `.pem` file safely.
- 🌍 Save your EC2’s **Public IPv4 DNS** — it's your way in!
- 🧹 **Delete resources** after use to **avoid unexpected AWS charges**.

> ✅> ⏱️ **Tip from experience:** Starting with the **EC2 instance first** made the Aurora setup easier to manage.  
> It took me around **2 hours** to complete the full project — including launching EC2, configuring Aurora, and connecting them together.

