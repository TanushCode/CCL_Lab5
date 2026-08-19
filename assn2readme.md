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
**The `CREATE` operation** in this Django/Wagtail application handles adding new bakery products to the DynamoDB table. It maps an incoming HTTP `POST` request payload to a DynamoDB item using the `boto3` SDK.

## 3. Implementation Details

#### API Endpoint
* **Method**: `POST`
* **URL**: `/api/products/`
* **Payload**: JSON object representing the product details.

#### Boto3 Method
The application uses the `put_item()` method from the `boto3` DynamoDB client library. This method creates a new item or replaces an old item with a new one.

#### Django View Function
Below is the structural implementation of the `CREATE` view within the Django application:

```python
import boto3
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt
import json

# Initialize the DynamoDB client using the EC2 instance role
dynamodb = boto3.client('dynamodb', region_name='ap-south-1')
TABLE_NAME = 'BakeryProducts'

@csrf_exempt
def create_product(request):
    if request.method == 'POST':
        try:
            # Parse the incoming JSON request body
            data = json.loads(request.body)
            
            # Map Python data types to explicit DynamoDB types
            dynamo_item = {
                'id': {'S': data['id']},
                'name': {'S': data['name']},
                'price': {'S': str(data['price'])},
                'available': {'BOOL': data['available']},
                'tags': {'L': [{'S': tag} for tag in data['tags']]},
                'details': {'M': {
                    'size': {'S': data['details']['size']},
                    'eggless': {'BOOL': data['details']['eggless']}
                }}
            }
            
            # Write the item to the DynamoDB table
            dynamodb.put_item(
                TableName=TABLE_NAME,
                Item=dynamo_item
            )
            
            return JsonResponse({'message': 'Product created successfully', 'id': data['id']}, status=201)
            
        except KeyError as e:
            return JsonResponse({'error': f'Missing required field: {str(e)}'}, status=400)
        except Exception as e:
            return JsonResponse({'error': str(e)}, status=500)
            
    return JsonResponse({'error': 'Method not allowed'}, status=405)
```

##  4.Request and Response Lifecycle

1. **Client Request**: The client sends a `POST` request to `/api/products/` with the product JSON structure in the body.
2. **Authentication**: The EC2 instance automatically fetches temporary security credentials via its attached IAM role.
3. **Validation**: The Django view extracts and structure-validates the fields.
4. **Execution**: The `put_item` call sends the typed payload to `ap-south-1`.
5. **Client Response**: Returns a `201 Created` status code upon success.
