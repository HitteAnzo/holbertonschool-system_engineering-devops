### **Explanation of Additional Elements**

1. **Why add 3 firewalls?**  
   Firewalls are added to:
   - Restrict unauthorized access to the servers.
   - Filter incoming and outgoing traffic based on security rules.
   - Protect against attacks like DDoS, brute force, and unauthorized access.

2. **Why serve traffic over HTTPS?**  
   HTTPS encrypts data transmitted between the user and the server, ensuring:
   - **Confidentiality**: Data cannot be intercepted or read by attackers.
   - **Integrity**: Data cannot be tampered with during transmission.
   - **Authentication**: Users can verify the identity of the server.

3. **Why add monitoring clients?**  
   Monitoring clients collect data to:
   - Track server performance (CPU, memory, disk usage).
   - Detect and resolve issues like traffic spikes or server failures.
   - Provide insights for scaling and optimizing the infrastructure.

4. **How does the monitoring tool collect data?**  
   Monitoring clients (e.g., Sumologic agents) collect metrics from the servers and send them to a centralized monitoring service. This data is then visualized in dashboards for analysis.

5. **How to monitor web server QPS (Queries Per Second)?**  
   - Use monitoring tools to track the number of requests handled by the web server per second.
   - Set up alerts for unusual spikes or drops in QPS.
   - Analyze trends to optimize server performance and scaling.

---

### **Issues with This Infrastructure**

1. **Terminating SSL at the Load Balancer Level**:  
   - **Issue**: If SSL is terminated at the load balancer, traffic between the load balancer and the web servers is unencrypted, exposing it to potential attacks.
   - **Solution**: Use end-to-end encryption by enabling SSL on the web servers as well.

2. **Only One MySQL Server Capable of Accepting Writes**:  
   - **Issue**: The Primary node is a single point of failure. If it fails, write operations cannot be performed until a new Primary is elected.
   - **Solution**: Implement a multi-primary database setup or use a distributed database system.

3. **Servers with All the Same Components**:  
   - **Issue**: If all servers run the same components (database, web server, application server), a failure in one component can affect the entire server.
   - **Solution**: Separate components across different servers to improve fault tolerance and scalability.