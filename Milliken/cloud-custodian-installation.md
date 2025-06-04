# Cloud Custodian Installation and Testing Process

## Installation Steps

1. System Requirements:
   - Python 3.x
   - pip
   - python3-venv

2. Clone the repository:
   ```bash
   git clone https://github.com/cloud-custodian/cloud-custodian.git
   cd cloud-custodian
   ```

3. Create and activate a virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

4. Install Cloud Custodian:
   ```bash
   pip install -e .
   ```

## Configuration Requirements

1. AWS Credentials:
   - AWS credentials must be configured either through:
     - AWS CLI configuration (`~/.aws/config` and `~/.aws/credentials`)
     - Environment variables (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_DEFAULT_REGION`)
   - Required permissions depend on the resources you want to manage

2. Basic Policy Structure:
   ```yaml
   policies:
     - name: policy-name
       resource: aws.resource-type
       filters:
         - type: filter-type
           key: value
       actions:
         - type: action-type
           key: value
   ```

## Testing Process

1. Create a test policy file:
   ```bash
   mkdir test-policies
   # Create your policy YAML file in test-policies directory
   ```

2. Run the policy:
   ```bash
   custodian run --output-dir output test-policies/your-policy.yml
   ```

## Common Issues and Requirements

1. Region Configuration:
   - AWS region must be specified either through:
     - AWS CLI configuration
     - Environment variable AWS_DEFAULT_REGION
     - Command line parameter --region

2. Output Directory:
   - The --output-dir parameter is required for running policies
   - This directory will contain logs and policy results

3. Authentication:
   - Proper AWS credentials with appropriate permissions are required
   - The tool will use the default AWS credential chain

## Additional Notes

- The tool supports dry-run mode with the --dryrun flag
- Policies can be validated without running using custodian validate
- Multiple AWS resources can be managed through different policies
- Supports various cloud providers (AWS, Azure, GCP) through different providers