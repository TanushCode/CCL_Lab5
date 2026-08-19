# Cloud Computing Lab 5 – Assignment 1
## Deploy and Connect Database for the Lab 4 EC2 Application

**Course:** Cloud Computing Lab  
**Semester:** V  
**Academic Year:** 2026–2027  
**Application:** Wagtail Bakery Demo  
**Cloud Platform:** Amazon Web Services (AWS)  
**Database:** Amazon RDS for PostgreSQL

---

## 1. Assignment Objective

The objective of Assignment 1 is to deploy the same database type used by the Lab 4 application on AWS and connect it to the existing application running on an Amazon EC2 instance.

The Lab 4 application is a Wagtail/Django Bakery Demo deployed on an Ubuntu EC2 instance. For this assignment, the application was connected to an **Amazon RDS PostgreSQL** database.

The implementation demonstrates:

- AWS RDS PostgreSQL deployment
- EC2-to-RDS connectivity
- Database authentication
- Django database configuration
- Django migrations against RDS
- Wagtail/Django database schema creation
- CRUD operations
- EC2 application service verification
- Database security configuration

---

# 2. System Architecture

```text
                         Internet / Client
                                |
                                |
                                v
                     +----------------------+
                     |     Ubuntu EC2        |
                     |                      |
                     |  Wagtail / Django    |
                     |  Bakery Demo         |
                     +----------+-----------+
                                |
                                | PostgreSQL
                                | connection
                                v
                     +----------------------+
                     |   Amazon RDS          |
                     |   PostgreSQL          |
                     |                      |
                     | Wagtail/Django DB    |
                     +----------------------+

```

# . Verification Summary
| Requirement                   | Status    |
| ----------------------------- | --------- |
| RDS PostgreSQL deployed       | Completed |
| EC2 application running       | Completed |
| EC2-to-RDS connectivity       | Completed |
| Database authentication       | Completed |
| Django RDS configuration      | Completed |
| Django migrations             | Completed |
| Wagtail/Django tables created | Completed |
| Create operation              | Completed |
| Read operation                | Completed |
| Update operation              | Completed |
| Delete operation              | Completed |
| Security configuration        | Completed |
| Wagtail systemd service       | Completed |


# . Result

The Lab 4 Wagtail Bakery Demo application was successfully connected to an Amazon RDS PostgreSQL database.

RDS deployment, database connectivity, authentication, Django configuration, migrations, Wagtail/Django schema creation, CRUD operations, security configuration, and EC2 application service operation were successfully verified.
