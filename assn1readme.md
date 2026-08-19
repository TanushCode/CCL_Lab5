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
3. AWS Services and Technologies
Service / Technology	Purpose
Amazon EC2	Hosts the Wagtail/Django application
Amazon RDS	Hosts the PostgreSQL database
Amazon VPC / Security Groups	Controls network connectivity
PostgreSQL	Relational database
Django	Web application framework
Wagtail	CMS/application framework
systemd	Manages the Wagtail application service

5. EC2 Application

The existing Lab 4 application is the Wagtail Bakery Demo.

Application directory:

/opt/wagtail-bakerydemo/app/bakerydemo

Python virtual environment:

/opt/wagtail-bakerydemo/app/bakerydemo/.venv

The application is managed using the systemd service:

wagtail.service

The Django application runs on:

0.0.0.0:8000
5. RDS PostgreSQL Deployment

An Amazon RDS PostgreSQL database was deployed for the Wagtail application.

The RDS database provides the persistent PostgreSQL backend for the Django/Wagtail application.

The following operations were performed:

Created the RDS PostgreSQL database.
Configured the required network/security access.
Connected from the EC2 instance to the RDS database.
Authenticated using the database user.
Configured Django to use the RDS database.
Applied Django migrations.
Verified Wagtail/Django tables in PostgreSQL.
Performed CRUD verification.
6. Network and Security Configuration

The RDS database requires PostgreSQL network connectivity from the EC2-hosted application.

The inbound security configuration for the Lab 4 environment was modified to permit the required database connection.

The intended architecture is:

EC2
 |
 | PostgreSQL connection
 |
 v
RDS PostgreSQL

The database should only be accessible through the required application/network path and should not be unnecessarily exposed to the public internet.

Evidence of the modified inbound rule is included in the submitted evidence document.

7. Database Authentication

Database connectivity was tested from the EC2 instance.

The following were successfully verified:

Connection to the RDS database
Database-user authentication
Successful database login
Django application database connectivity

This confirmed that the EC2 application environment could communicate with the RDS PostgreSQL database.

8. Django Database Integration

The Wagtail/Django application was configured to use the Amazon RDS PostgreSQL database.

The application was then tested using Django's database functionality.

Django migrations were executed against the RDS database.

Successful migrations confirmed that Django could communicate with PostgreSQL and create the required application schema.

9. Django and Wagtail Database Schema

The database schema was created using Django migrations.

The resulting PostgreSQL database contains tables required by Django and Wagtail, including components for:

Authentication
Administration
Sessions
Wagtail Core
Wagtail Admin
Wagtail Images
Wagtail Documents
Wagtail Search
Wagtail Users
Application-specific models

The Wagtail/Django tables were inspected in PostgreSQL as part of the database verification.

10. Systemd Service Configuration

The Wagtail application is managed using systemd.

The service configuration was inspected using:

sudo systemctl cat wagtail.service

Service properties were inspected using:

sudo systemctl show wagtail.service

The service environment was inspected using:

sudo systemctl show wagtail.service --property=Environment

The Wagtail service was successfully running on the EC2 instance after the RDS integration.

11. Django Migration

After configuring the RDS database, Django migrations were executed.

The migrations successfully created the required database tables in PostgreSQL.

This verified the complete application-to-database path:
```
Wagtail / Django
       |
       v
Amazon RDS PostgreSQL
       |
       v
Django / Wagtail Tables
```
12. CRUD Verification

The application/database implementation was tested for all four required CRUD operations.

Create

A new record was successfully created in the PostgreSQL database.

Read

Stored data was successfully retrieved from the PostgreSQL database.

Update

An existing record was successfully modified.

Delete

An existing record was successfully deleted.

Therefore, all required CRUD operations were demonstrated:

Create → Read → Update → Delete

CRUD verification evidence is included separately with the submission.

13. Evidence Submitted

The separate evidence document contains screenshots showing:

Database
Created RDS database
Database configuration
Security
Modified inbound rule for Lab 4 instance
Connectivity
Connection to database succeeded
Login to database user
Verify Django RDS connection
Application Service
sudo systemctl cat wagtail.service
sudo systemctl show wagtail.service
sudo systemctl show wagtail.service --property=Environment
Wagtail service running on EC2
Migration
Successful Django migration to RDS
Database Schema
Wagtail Django tables in PostgreSQL
CRUD
Amazon RDS PostgreSQL CRUD operation verification

14. Verification Summary
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


15. Result

The Lab 4 Wagtail Bakery Demo application was successfully connected to an Amazon RDS PostgreSQL database.

RDS deployment, database connectivity, authentication, Django configuration, migrations, Wagtail/Django schema creation, CRUD operations, security configuration, and EC2 application service operation were successfully verified.
