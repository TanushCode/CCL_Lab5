# Cloud Computing Lab 5 – Assignment 2

## NoSQL Database Integration using Amazon DynamoDB

**Course:** Cloud Computing Lab  
**Semester:** V  
**Academic Year:** 2026–2027  
**Application:** Wagtail Bakery Demo  
**Database:** Amazon DynamoDB  
**AWS Region:** ap-south-1  
**Cloud Platform:** Amazon Web Services (AWS)

---

## 1. Objective

The objective of Assignment 2 is to use the database type opposite to the one used in Assignment 1.

For Assignment 2, the Wagtail Bakery Demo application running on an Ubuntu EC2 instance was integrated with Amazon DynamoDB.

The implementation demonstrates:

- DynamoDB table deployment
- EC2 IAM Role based AWS access
- boto3 integration
- Django API integration
- REST API endpoints
- Create, Read, Update and Delete operations
- Five required DynamoDB attribute types
- EC2 application operation
- Secure AWS authentication without hardcoded credentials

---

## 2. Architecture

```text
                         Internet / Client
                                |
                                v
                     +----------------------+
                     |     Ubuntu EC2       |
                     |                      |
                     |  Wagtail / Django    |
                     |      REST API        |
                     +----------+-----------+
                                |
                                | boto3
                                |
                                v
                     +----------------------+
                     |   IAM Instance Role  |
                     |                      |
                     | BakeryDemoDynamoDB  |
                     |       Role          |
                     +----------+-----------+
                                |
                                | AWS API
                                v
                     +----------------------+
                     |   Amazon DynamoDB    |
                     |                      |
                     |   BakeryProducts    |
                     +----------------------+

```
## 3. AWS Resources### EC2Application: Wagtail Bakery DemoOperating System: UbuntuApplication server: Django/WagtailApplication API port: 8000### DynamoDBTable name: BakeryProductsRegion: ap-south-1Database type: NoSQLPartition key: idThe table is accessed by the EC2 instance through an attached IAM role.## 4. DynamoDB Table Design

TableTable Name: BakeryProducts
Partition Key: id
Partition Key Type: StringExample item:{
  "id": "P002",
  "name": "Red Velvet Cake",
  "price": "550.00",
  "available": true,
  "tags": [
    "cake",
    "red-velvet"
  ],
  "details": {
    "size": "1kg",
    "eggless": false
  }
}## 5. DynamoDB DatatypesThe BakeryProducts item demonstrates at least five DynamoDB attribute types.AttributeDynamoDB TypeExampleidString (S)"P002"nameString (S)"Red Velvet Cake"priceString (S)"550.00"availableBoolean (BOOL)truetagsList (L)["cake", "red-velvet"]detailsMap (M){"size":"1kg","eggless":false}details.egglessBoolean (BOOL)falseThe required DynamoDB types demonstrated by the application are:String (S)    ✓
Boolean (BOOL) ✓
List (L)      ✓
Map (M)       ✓The item also contains multiple attributes suitable for demonstrating DynamoDB's flexible NoSQL schema.## 6. IAM SecurityThe EC2 instance uses an IAM role instead of hardcoded AWS credentials.The IAM role attached to the EC2 instance provides DynamoDB permissions required by the application.The application uses the EC2 instance role through boto3.Required operations include:dynamodb:PutItem
dynamodb:GetItem
dynamodb:UpdateItem
dynamodb:DeleteItem
dynamodb:Scan
dynamodb:Query
dynamodb:DescribeTableThe application therefore does not require an AWS access key or secret access key stored inside the source code.## 7. Application APIThe Django application exposes the following API endpoints:GET     /api/products/
POST    /api/products/
GET     /api/products/&lt;product_id&gt;/
PUT     /api/products/&lt;product_id&gt;/
DELETE  /api/products/&lt;product_id&gt;/The API communicates with the BakeryProducts DynamoDB table.## 8. CRUD Implementation### CREATEA product was created using:POST /api/products/Example product:ID: P002
Name: Red Velvet Cake
Price: 550.00
Available: trueThe API returned:HTTP 201 Createdwith:{
  "message": "Product created"
}### READProducts were retrieved using:GET /api/products/The API successfully returned the DynamoDB items.A specific product can also be retrieved using:GET /api/products/P002/

          
            
          
        
  
        
    

UPDATEThe product was updated using:PUT /api/products/P002/The product name and price were modified.Example updated values:Name: Red Velvet Cake - Updated
Price: 600.00The API returned:HTTP 200 OKwith the updated DynamoDB item.### DELETEThe product was deleted using:DELETE /api/products/P002/The API returned:HTTP 200 OKwith:{
  "message": "Product deleted"
}Therefore:CREATE  ✓
READ    ✓
UPDATE  ✓
DELETE  ✓## 9. Connection VerificationThe EC2 instance successfully accessed DynamoDB using the attached IAM role.The following DynamoDB tables were successfully visible from the EC2 environment:BakeryProducts
GamePlayer
testThis verified that the EC2 IAM role was functioning correctly.## 10. EvidenceThe submitted evidence contains screenshots showing:DynamoDB BakeryProducts tableTable partition-key configurationDynamoDB sample itemEC2 IAM role configurationSuccessful DynamoDB access from EC2Wagtail application running on EC2API CREATE operationAPI READ operationAPI UPDATE operationAPI DELETE operationFive required DynamoDB datatype evidenceThe screenshots are provided separately as assignment evidence.## 11. ResultThe Wagtail Bakery Demo application running on EC2 was successfully integrated with Amazon DynamoDB.The application uses the EC2 IAM role for AWS authentication and performs all mandatory CRUD operations through a Django API.The DynamoDB data model demonstrates multiple DynamoDB attribute types including String, Boolean, List, and Map.### Assignment 2 StatusDynamoDB Deployment             ✓
EC2 IAM Role                    ✓
No Hardcoded AWS Keys           ✓
Application Connection          ✓
CREATE                          ✓
READ                            ✓
UPDATE                          ✓
DELETE                          ✓
Multiple DynamoDB Datatypes     ✓
