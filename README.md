# AWS VPC Peering Project

## EWB Cloud Labs | AWS Internship Batch 1

**Student Name:** Harsha Vardhan Arle  
**Project:** VPC Peering  
**AWS Region:** Asia Pacific (Mumbai) - `ap-south-1`  
**Platform:** Amazon Web Services (AWS)

---

## 1. Project Overview

This project demonstrates how to establish private network connectivity between two Amazon Virtual Private Clouds (VPCs) using **VPC Peering**.

The implementation includes two VPCs, public and private subnets, EC2 instances, route tables, security groups, and a bastion host.

Connectivity between private EC2 instances was tested in both directions using ICMP (ping), and SSH access was verified through the bastion host.

## 2. Project Objectives

- Create and configure two Amazon VPCs.
- Configure public and private subnets.
- Set up an Internet Gateway for VPC A.
- Establish VPC Peering between VPC A and VPC B.
- Configure route tables and subnet associations.
- Implement security-group rules.
- Access private EC2 instances through a bastion host.
- Verify bidirectional connectivity.
- Perform controlled failure and recovery testing.

## 3. AWS Architecture

The project uses the following network design:

| Resource | Name | CIDR / IP Address |
|---|---|---|
| VPC A | `ewb-vpc-a` | `10.10.0.0/16` |
| VPC B | `ewb-vpc-b` | `10.20.0.0/16` |
| Public Subnet | `ewb-a-public` | `10.10.1.0/24` |
| Private Subnet A | `ewb-a-private` | `10.10.2.0/24` |
| Private Subnet B | `ewb-b-private` | `10.20.1.0/24` |
| Internet Gateway | `ewb-igw-a` | Attached to VPC A |
| VPC Peering | `ewb-a-b-peer` | Active |

## 4. EC2 Instances

| Instance | Private IP | Purpose |
|---|---|---|
| Bastion Host | `10.10.1.10` | Secure SSH entry point |
| App-A | `10.10.2.10` | Private application instance in VPC A |
| App-B | `10.20.1.10` | Private application instance in VPC B |

**Operating System:** Amazon Linux 2023  
**Instance Type:** `t3.micro`

## 5. Networking Configuration

### VPC Peering

A VPC Peering connection was established between VPC A and VPC B. The connection status was verified as **Active**.

### Route Tables

- Public route table: Internet Gateway route and VPC B peering route.
- Private route table A: Route to VPC B through the peering connection.
- Private route table B: Route to VPC A through the peering connection.

### Security Groups

Security groups were configured to allow:

- SSH access to the bastion host.
- SSH access to private instances through the bastion host.
- ICMP Echo Request traffic between App-A and App-B.
- Required outbound traffic.

## 6. Connectivity Testing

The following tests were successfully performed:

| Test | Result |
|---|---|
| VPC Peering status | Active |
| SSH to Bastion Host | Successful |
| SSH to App-A | Successful |
| SSH to App-B | Successful |
| App-A to App-B ping | Successful |
| App-B to App-A ping | Successful |
| Controlled ICMP failure | Verified |
| ICMP recovery after restoring rule | Successful |

Both ping tests achieved **0% packet loss** after the security-group rules were correctly configured.

## 7. Controlled Failure and Recovery

A controlled failure test was performed by temporarily removing the inbound ICMP Echo Request rule on App-B.

- App-A could no longer ping App-B.
- The test showed 100% packet loss.
- The ICMP rule was restored.
- Connectivity was successfully recovered.

This demonstrated the impact of security-group rules on network communication.

## 8. Project Learning Outcomes

Through this project, I gained practical experience in:

- Amazon VPC creation and configuration.
- Public and private subnet management.
- Internet Gateway configuration.
- VPC Peering implementation.
- Route table configuration.
- Security-group management.
- Bastion host and SSH ProxyJump access.
- Network connectivity troubleshooting.
- Controlled failure and recovery testing.

## 9. Repository Structure

```text
EWB-VPC-Peering-Project/
│
├── README.md
├── Harsha_Vardhan_Arle_EWB_VPC_Peering.pdf
├── AWS-Architecture.jpeg
│
└── Screenshots/
    ├── VPC-Details.png
    ├── Subnet-Details.png
    ├── VPC-Peering.png
    ├── Route-Tables.png
    ├── Security-Groups.png
    ├── App-A-to-App-B-Ping.png
    ├── App-B-to-App-A-Ping.png
    ├── SSH-App-A.png
    ├── SSH-App-B.png
    ├── Controlled-Failure.png
    └── Recovery-Test.png
```

*Note: Add only the files and screenshots that are actually included in the repository.*

## 10. Conclusion

The AWS VPC Peering project was successfully implemented and tested. Private communication between two separate VPCs was verified using bidirectional ping tests, and secure SSH access to private EC2 instances was demonstrated through a bastion host.

This project provided practical knowledge of AWS networking, secure connectivity, and cloud infrastructure management.

---

**Submitted by:** Harsha Vardhan Arle  
**Internship:** EWB Cloud Labs - AWS Internship Batch 1
