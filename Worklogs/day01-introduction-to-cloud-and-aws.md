# Introduction to Cloud and AWS

## 1. What is Cloud computing?

Cloud computing is the work that we distribute IT resources on demand over the Internet with pay-as-you-go policy. This means, instead of building systems such as servers, networking devices, etc. by ourselves, we just need to send a request to providers, and say we need a server with this configuration, they will provide us with a virtual server and the info to use it.

## 2. Advantages of Cloud computing

- **Pay-as-you-go** method helps us to *optimize the cost*.
- **Speed up** the development of our software, since we can focus on developing applications instead of hardware installation.
- **Scalability**: Resources can be scaled up or down based on our demand. It is not fixed over time.
- **Flexibility**: Add or remove resources whenever we want.

## 3. What makes AWS different?

- **AWS** is the leading service 13 times in a row (by the end of 2023, evaluated by Gartner, Inc.).
- Customers will pay less over time. The more they use, the less they pay. AWS takes advantage of economies of scale to lower infrastructure costs → *differences in vision and culture*.
- **Leadership principles**: Customer obsession, ownership, invent and simplify, "are right, a lot", learn and be curious, hire and develop the best.

## 4. How can we start our journey?

- Befriend and learn from others.
- Enroll in an AWS account as soon as possible and experience it through the Free Tier.

## 5. AWS infrastructures

- **Availability Zone (AZ)**: Includes one or more data centers. Designed to prevent fault isolation. Between two AZs is a high-speed private connection. AWS encourages deploying apps in at least two AZs.
- **Region**: Includes at least 3 Availability Zones. Each region connects with others via AWS’s backbone network. Data and services on regions are independent of each other.
- **Edge Locations (POP)**: Smaller data centers located worldwide where AWS services are deployed to deliver content to end-users with low latency. Used for content delivery through Amazon CloudFront (CDN), Route 53 (DNS), Web Application Firewall (WAF), etc.

## 6. AWS services management tool

- **AWS Management Console**:
  - We can log in using a root account or an IAM User (a child account to utilize AWS services).
  - After login, we can search for the services we want.
  - The support center is located on the left.

- **AWS Command Line Interface (CLI)**: Open-source tool that allows us to use AWS services via terminal or command prompt.

- **AWS SDK**: Simplifies the use of AWS services for applications by providing a consistent and familiar set of libraries for development teams.
