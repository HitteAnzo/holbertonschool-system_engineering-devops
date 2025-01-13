### **Explanation of Additional Elements**

1. **Why add 2 servers?**  
   Adding two servers improves **reliability** and **scalability**. If one server fails, the other can handle traffic, reducing downtime. It also allows for better distribution of incoming traffic.

2. **Why add a load balancer (HAproxy)?**  
   The load balancer distributes traffic evenly across the web servers, preventing any single server from being overwhelmed. It also improves **availability** and **fault tolerance**.

3. **What distribution algorithm is the load balancer configured with?**  
   The load balancer uses the **round-robin algorithm**, which distributes requests sequentially across the available servers. For example:
   - Request 1 → Server 1
   - Request 2 → Server 2
   - Request 3 → Server 1
   - Request 4 → Server 2  
   This ensures an even distribution of traffic.

4. **Is the load balancer enabling an Active-Active or Active-Passive setup?**  
   - **Active-Active**: Both servers are actively handling traffic simultaneously. This setup improves **scalability** and **resource utilization**.
   - **Active-Passive**: Only one server is active, while the other is on standby. If the active server fails, the passive server takes over. This setup improves **fault tolerance** but underutilizes resources.  
   
   In this infrastructure, the load balancer is configured for an **Active-Active** setup.

5. **How does a Primary-Replica (Master-Slave) database cluster work?**  
   - The **Primary node** handles all write operations (INSERT, UPDATE, DELETE) and replicates changes to the **Replica node**.
   - The **Replica node** handles read operations (SELECT) and stays in sync with the Primary node.  
   This setup improves **read scalability** and provides **data redundancy**.

6. **What is the difference between the Primary and Replica nodes in regard to the application?**  
   - The **Primary node** is used for write operations, ensuring data consistency.
   - The **Replica node** is used for read operations, reducing the load on the Primary node and improving performance.

---

### **Issues with This Infrastructure**

1. **Single Points of Failure (SPOF)**:  
   - **Load Balancer**: If the load balancer fails, traffic cannot be distributed, causing downtime.
   - **Primary Database Node**: If the Primary node fails, write operations cannot be performed until a new Primary is elected.

2. **Security Issues**:  
   - **No Firewall**: The infrastructure is vulnerable to attacks (e.g., DDoS, unauthorized access).
   - **No HTTPS**: Data transmitted between the user and the server is not encrypted, exposing sensitive information.

3. **No Monitoring**:  
   Without monitoring, it is difficult to detect and resolve issues like server failures, traffic spikes, or performance bottlenecks.