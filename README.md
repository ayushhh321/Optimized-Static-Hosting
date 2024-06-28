# Hosting a Static Website on Amazon S3

## Why Choose S3 Over Other AWS Services?

- **S3 vs. EC2**: S3 is designed specifically for static content hosting, offering scalability, high availability, and durability with minimal management. EC2 is more suited for dynamic applications and requires more maintenance.
- **S3 vs. Amplify**: AWS Amplify is a full-stack platform, more suited for modern web and mobile applications with backend support. For purely static sites, S3 is simpler and more cost-effective.
- **S3 vs. Elastic Beanstalk**: Elastic Beanstalk is used for deploying and managing applications within a variety of environments. It’s overkill for static sites, where S3 offers a simpler, more efficient solution.
- **S3 vs. Lightsail**: Lightsail is similar to EC2 but more user-friendly, with virtual servers and other resources. It's better for simple web applications rather than just static file hosting.

## Steps to Host Your Static Website on S3

### 1. Create an S3 Bucket

1. **Login to AWS Management Console**.
2. Navigate to **S3**.
3. Click on **Create bucket**.
4. Enter a unique bucket name.
5. Choose the appropriate region.
6. Uncheck **Block all public access** (we'll configure specific public access settings later).

### 2. Configure Bucket Permissions and Versioning

- **ACL Public Access**:
  - Ensure the bucket is publicly accessible to serve content over the internet.
  - This can be managed in the Permissions tab of your S3 bucket settings.

- **Bucket Versioning** (Optional):
  - Enable versioning to maintain versions of your objects, which can help with rollback and recovery.

### 3. Set Bucket Policy

- Navigate to the **Permissions** tab of your S3 bucket.
- Add a bucket policy to allow public read access. Use the policy generator for this.

#### Example Bucket Policy:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
```
## 4. Use AWS CLI to Upload Files

Uploading files manually can lead to incorrect file structure and path errors in your codebase. To avoid this, use the AWS CLI.

### Install AWS CLI:

Follow the [official AWS CLI installation guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).

### Configure AWS CLI:

```bash
aws configure
```
### Sync Command to Upload Files:

```bash
aws s3 sync /path/to/your/local/website s3://your-bucket-name
```
## 5. Configure Static Website Hosting

- Go to your S3 bucket properties.
- Under Static website hosting, click Edit.
- Select Enable.
- Specify the index document (e.g., index.html).
- Optionally, specify an error document (e.g., error.html).

