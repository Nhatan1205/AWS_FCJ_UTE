#  Continue
## 5. Lab 03-01.4: NAT Gateway

A NAT Gateway allows instances in a private subnet to access the internet while blocking inbound traffic from the internet.

- **NAT Gateway vs. NAT Instance:** NAT Gateways provide a more scalable and higher-availability solution compared to NAT instances.
- **One-Way Traffic:** The traffic flows in one direction—from private EC2 instances to the internet. The NAT gateway cannot allow inbound traffic from the internet.
- **Costing:** Pricing is based on usage hours, data processing, and data transfer, making it more expensive than NAT instances but offering better performance and availability.

## 6. Lab 03-02.1: Security Group

Security Groups are virtual firewalls that control inbound and outbound traffic for your EC2 instances.

- **Stateful Nature:** If you allow inbound traffic on a specific port, the return traffic is automatically allowed, regardless of outbound rules.
- **Default Security Group:** When you create a new VPC, a default security group is automatically created. This group blocks all inbound traffic and allows all outbound traffic unless changed.
- **Custom Security Group:** You can create custom security groups with specific rules, such as allowing traffic on port 80 (HTTP) or port 22 (SSH).

## 7. Lab 03-02.2: Network ACLs (NACLs)

Network ACLs are a layer of security that controls traffic at the subnet level, unlike Security Groups, which control traffic at the instance level.

- **Stateless Nature:** NACLs are stateless, meaning that inbound and outbound traffic must be explicitly allowed. If traffic is allowed in, it does not automatically allow outbound traffic.
- **Default NACL:** Each VPC comes with a default NACL that allows all inbound and outbound traffic. You can modify or create additional NACLs to control traffic more finely.
- **Associating NACLs with Subnets:** NACLs must be explicitly associated with subnets. If a subnet is not associated with a custom NACL, it will use the default NACL.
- **Inbound and Outbound Rules:** NACLs allow both allow and deny rules, which provides more granular control over traffic than security groups.
