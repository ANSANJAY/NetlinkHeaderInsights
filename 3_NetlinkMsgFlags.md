## 📝 Netlink Message Flags

### 🔍 Introduction

Netlink message flags are used to convey additional information to the recipient of the message. They play an important role in the communication between user space and kernel space.

### 🏳 Flags Overview

1. **Request Flag**: Set by one party when requesting another party to perform a specific action. Example: When user space asks kernel space to create a new routing table entry.
2. **Create Flag**: Indicates the intention to create a new resource in the kernel. This often refers to a new entry.
3. **Exclude Flag**: Accompanies the Create flag. If set, it signals the kernel that if the resource being requested to create already exists, return an error.
4. **Replace Flag**: Used to indicate the need to replace an existing resource in the kernel.
5. **Append Flag**: Signals the kernel to add data to an existing configuration, like adding more data to a linked list.
6. **Dump Flag**: Requested by user space when it wants the kernel to send back all its data. If the data can't fit in one netlink message, the kernel sends the data in multiple cascaded messages.
7. **Multi Flag**: Indicates to the recipient that another netlink message follows. Used in cascaded multi-part netlink messages.
8. **Acknowledgement Flag**: Used when feedback from the recipient is required. The feedback can be in the form of a Netlink message type like 'no operation' or 'error'.

### 📁 File Reference

All these flags are defined in the file:
```
Linux/netlink.h
```

Between lines 54 to 78, a variety of flags can be found, with the discussed flags being the most commonly used ones.

### 🛠 Practical Application

Throughout the Netlink project, these flags will be exercised. Based on these flags, the recipient, whether it's in user space or kernel space, will determine the necessary action to take.

---

## ❓ Interview Questions about Netlink Message Flags

**Q1**: What is the purpose of the Exclude flag in netlink messages? 🤔
> **Answer**: The Exclude flag is set by the user space application when requesting the Linux kernel module to create a new resource. By setting this flag, it instructs the kernel to return an error if the requested resource already exists. Essentially, it's a way to ensure uniqueness.

**Q2**: How does the kernel handle situations where data requested by user space can't fit in a single netlink message? 💼
> **Answer**: The kernel opts to chunk the message and sends the data to the user space in multiple parts or cascaded netlink messages. This approach becomes necessary when, for instance, the number of entries being sent could be very large, making it difficult to obtain a contiguous buffer.

**Q3**: Describe the significance of the Acknowledgement flag in a netlink message. 🚩
> **Answer**: The Acknowledgement flag, when set, signifies a request for feedback from the recipient. Upon receiving a message with this flag, the kernel can reply with either a 'no operation' Netlink message or a Netlink 'error' message, providing the necessary feedback to the sender.

**Q4**: In what scenarios might the Multi flag be used in cascaded multi-part netlink messages? 🔄
> **Answer**: The Multi flag is used in cascaded multi-part netlink messages to indicate to the recipient that another netlink message follows. For instance, if there are three cascaded netlink messages, the first two will have this flag set to inform the recipient to expect another following message.

**Q5**: Why might a user space application set the Append flag when communicating with the kernel? ➕
> **Answer**: The Append flag signals the kernel to add more data to an existing configuration, such as adding more data to an already existing linked list. Thus, a user space application might set the Append flag when it wants to add to or augment data that's already present in the kernel.

---

Note: It's essential to dive deeper into the `Linux/netlink.h` file and practice using these flags in real scenarios to get more familiarized and develop confidence when handling netlink messages.
