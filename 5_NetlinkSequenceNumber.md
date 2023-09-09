## 📝 Sequence Number in Netlink Communication - Detailed Notes

### 🌐 Introduction

Understanding the `sequence number` and `PID` fields is crucial before diving into the practical implementation of interaction between user space and kernel space using Netlink.

### 🚀 The Role of Sequence Number

1. **Purpose**: The sequence number serves as a unique identifier when a user space application sends a netlink request message to the kernel space.
  
2. **Acknowledgment Flag**:
   - When the user space application sets an acknowledgment flag in the netlink message, it expects a feedback or reply from the kernel space.
   - If the acknowledgment flag is set, the kernel space responds with a confirmation message, retaining the same sequence number that was provided in the original request.

3. **Correlation between Requests and Replies**:
   - The sequence number enables the user space application to correlate which Netlink reply corresponds to which Netlink request, especially when multiple requests are pending.
   
4. **Illustration**:
   - **Scenario**: 
     - A user space application sends multiple requests (`R1`, `R2`, `R3`) with sequence numbers `6`, `7`, and `8` respectively to the kernel space.
     - The kernel processes `R2` first and sends a reply.
   - **Challenge**: 
     - How can the user space application determine which request this reply corresponds to?
   - **Solution**: 
     - The kernel includes the same sequence number (`7` in this case) in its reply, helping the user space application deduce that the reply is for request `R2`.

5. **Incremental Sequence Numbers**:
   - It's imperative that the user space application sets the sequence number as an always increasing integer, ensuring each request is distinctly identifiable.

---

## ❓ Interview Questions about Sequence Number in Netlink Communication

**Q1**: What is the primary purpose of the sequence number in Netlink communication? 🤖
> **Answer**: The sequence number acts as a unique identifier, allowing the user space application to correlate Netlink replies with their respective Netlink requests, especially when multiple requests are made to the kernel space.

**Q2**: How does the kernel space handle the sequence number when replying to a request from the user space? 🔄
> **Answer**: When the kernel space sends a reply to the user space application, it uses the same sequence number that was specified in the original request. This aids the user space application in identifying which request the reply pertains to.

**Q3**: In the provided illustration, which request was processed first by the kernel space, and what was its sequence number? 🧩
> **Answer**: In the illustration, the request `R2` was processed first by the kernel space, and its sequence number was `7`.

**Q4**: Why is it essential for the sequence number to be an ever-increasing integer in Netlink communication? 📈
> **Answer**: Setting the sequence number as an ever-increasing integer ensures that each request is distinctly identifiable, avoiding any overlaps or confusion in correlating requests and replies.

**Q5**: How does the acknowledgment flag influence the use of the sequence number in a Netlink message? 🚩
> **Answer**: When the acknowledgment flag is set in a Netlink message sent by the user space application, it indicates an expectation for feedback or reply from the kernel space. In such cases, the sequence number becomes even more critical, as the kernel's reply will contain the same sequence number, facilitating easy correlation of requests and responses.

---

Properly handling the sequence number in Netlink communication ensures smooth and organized interaction between user space applications and the kernel space.
