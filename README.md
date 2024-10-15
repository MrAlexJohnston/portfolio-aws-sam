# Portfolio AWS SAM - Lambda Functions Deployed via AWS CDK

This project demonstrates the deployment of serverless applications using AWS SAM (Serverless Application Model) integrated into an AWS CDK pipeline. The Lambda functions defined in the SAM template are deployed within private subnets and secured with specified security groups, making use of DynamoDB for data storage.

## Project Structure

- **src/**: Contains the source code for Lambda functions.
  - `handlers/`: Defines handlers for the Lambda functions, including:
    - `get-all-items.mjs`: Handler to retrieve all items from the DynamoDB table.
    - `get-by-id.mjs`: Handler to retrieve a specific item by ID.
    - `put-item.mjs`: Handler to insert an item into the DynamoDB table.
- **events/**: Defines events to invoke the Lambda functions (e.g., API Gateway).
- **template.yaml**: AWS SAM template defining the resources and deployment configuration.
- **tests/**: Contains unit tests for the Lambda functions.

## AWS SAM Resources

The SAM template (`template.yaml`) defines the following resources:

- **Lambda Functions**:
  - `getAllItemsFunction`: Fetches all items from a DynamoDB table.
  - `getByIdFunction`: Fetches an item by its ID.
  - `putItemFunction`: Adds a new item to the DynamoDB table.
  
- **DynamoDB Table**:
  - `SampleTable`: A simple DynamoDB table with an `id` as the primary key.

- **API Gateway**:
  - Configured to expose HTTP methods (GET, POST) for the Lambda functions.

## CDK Integration

The deployment process is managed via AWS CDK. The SAM application is integrated into an AWS CDK pipeline that automates the deployment of Lambda functions into private subnets using the security group and subnet IDs defined in the template.

### VPC Configuration

The Lambda functions are deployed in private subnets within the VPC, and secured using a designated security group. The following parameters are used:

- **SecurityGroupId**: Security group ID for the Lambda functions.
- **SubnetId1, SubnetId2, SubnetId3**: Subnet IDs where the Lambda functions will be deployed.

These parameters are referenced in the SAM template to ensure the Lambda functions are deployed securely in your VPC.

## Deployment Instructions

### Prerequisites

- AWS CLI configured with appropriate permissions.
- AWS CDK Toolkit installed (`npm install -g aws-cdk`).
- Node.js and NPM installed.

### Steps

1. **Install Dependencies**  
   Run `npm install` to install the necessary packages for both AWS CDK and Lambda functions.

2. **Build the CDK Project**  
   Run `npm run build` to compile the CDK and SAM TypeScript/JavaScript code.

3. **Deploy Using AWS CDK**  
   Run `npx cdk deploy` to deploy the entire stack, including the AWS SAM Lambda functions.

4. **Test the API**  
   After deployment, the API Gateway endpoint URL will be outputted. You can use this URL to test the GET and POST methods for interacting with the DynamoDB table.

## Example API Endpoints

After deployment, you can interact with the Lambda functions via API Gateway using the following routes:

- `GET /`: Fetch all items from the DynamoDB table.
- `GET /{id}`: Fetch an item by its ID.
- `POST /`: Add a new item to the DynamoDB table.

## Testing

Unit tests for the Lambda functions are located in the `tests/` directory. Use the following command to run the tests:

```bash
npm run test
