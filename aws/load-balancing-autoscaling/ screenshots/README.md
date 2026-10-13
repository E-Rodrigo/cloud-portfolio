### 1. Application Load Balancer Configuration
Application Load Balancer creation and network configuration across two Availability Zones.

The load balancer provides a single entry point for incoming HTTP traffic and distributes requests across registered application instances.

![Load Balancer Configuration](./01-load-balancer-configuration.jpeg)

### 2. Launch Template Configuration
Creation of the EC2 Launch Template.

The Launch Template defines the configuration used to provision application instances, including the custom AMI, instance type, and security group.

![Launch Template Configuration](./02-launch-template-configuration.jpeg)

### 3. Auto Scaling Group Configuration

Creation and configuration of the EC2 Auto Scaling group.

The group is configured to manage instance capacity across two private subnets in separate Availability Zones, with a minimum capacity of two instances and a maximum capacity of four.

![Auto Scaling Group Configuration](./03-auto-scaling-group-configuration.jpeg)

### 4. Initial EC2 Instances Provisioned

EC2 instances launched and managed by the Auto Scaling group.

The initial instances are provisioned using the Launch Template and registered with the load balancer's target group, enabling health checks and traffic distribution.

![Initial EC2 Instances](./04-initial-ec2-instances.jpeg)

### 5. Load Test Execution

Execution of the application's load testing functionality.

The test generates additional CPU workload to evaluate the Auto Scaling policy's response to increased demand.

![Load Test Execution](./05-load-test-execution.jpeg)

### 6. Scale-Out Event Triggered by High CPU Utilization

The Auto Scaling group launches an additional EC2 instance following increased CPU utilization.

Amazon CloudWatch detects that average CPU utilization has exceeded the configured 50% target, triggering the scale-out process.

![Auto Scaling Scale Out Event](./06-auto-scaling-scale-out-event.jpeg)

### 7. CloudWatch Alarm During the Load Test

CloudWatch alarm state after the load test increases CPU utilization.

The alarm reflects the elevated workload and the scaling policy's response to increased demand.

![CloudWatch Alarm During Load Test](./07-cloudwatch-alarm-during-load-test.jpeg)

### 8. CloudWatch Alarm Returns to a Normal State

CloudWatch alarm state after the additional instance becomes available.

Following the scaling activity and subsequent metric evaluation, the alarm returns to its normal state, indicating that the alarm condition is no longer being met.

![CloudWatch Alarm Normalized](./08-cloudwatch-alarm-normalized.jpeg)

### 9. EC2 Instance Launch Activity

EC2 instances being launched following the Auto Scaling group's scaling activity.

This view documents the instance provisioning process associated with the scaling event and helps illustrate how the infrastructure responds to workload changes.

![EC2 Instance Launch Activity](./09-ec2-instance-launch-activity.jpeg)
