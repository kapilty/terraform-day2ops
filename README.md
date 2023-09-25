# AWS ASG Rolling Update with Terraform 
This repository offers robust Terraform configurations for ASG infrastructure, showcasing AWS deployment and scaling best practices. Use it to deploy new instances with minimal downtime using rolling updates.

## Prerequisites  
Before you begin, make sure you have the following prerequisites:  
- [Terraform](https://www.terraform.io/downloads.html) installed on your local machine.
- Appropriate AWS credentials configured for Terraform.

## Usage  

1. Clone this repository to your local machine:     

    `git clone https://github.com/madgicaltechdom/terraform-as-rolling-updates.git`

    `cd terraform-as-rolling-updates `

2.  Initialize Terraform in the project directory:
    
    `terraform init`
    
3.  Review and customize the `vars.tf` file with your AWS configuration and desired values.
    
4.  Apply the Terraform configuration:
    
    `terraform apply`
    
5.  Confirm the changes by typing `yes` when prompted.
    
6.  Terraform will provision the ASG and Launch Template according to your configuration.
    
7.  Change the [AMI](https://github.com/madgicaltechdom/terraform-as-rolling-updates/blob/main/ami.tf#L5-L15) according to your requirements
8.  Apply the Terraform configuration:
    
    `terraform apply`

9. You would noticed that the ASG is deploying the latest AMI with minimal downtime.    
    

Configuration
-------------

### `aws_launch_template`

The `aws_launch_template` resource defines the launch template used for the instances in the Autoscaling Group.

*   `name`: The name of the launch template.
*   `image_id`: The ID of the AMI (Amazon Machine Image) to use.
*   `instance_type`: The instance type for the instances.
*   `key_name`: The name of the SSH key pair.
*   `user_data`: The user data script for instances.
*   `vpc_security_group_ids`: The security group IDs.
*   `tag_specifications`: Tags for the instances.

### `aws_autoscaling_group`

The `aws_autoscaling_group` resource defines the Autoscaling Group.

*   `name`: The name of the Autoscaling Group.
*   `desired_capacity`: The desired number of instances.
*   `health_check_grace_period`: The health check grace period.
*   `health_check_type`: The health check type.
*   `max_size`: The maximum number of instances.
*   `min_size`: The minimum number of instances.
*   `target_group_arns`: The ARNs of the target groups.
*   `vpc_zone_identifier`: The subnet IDs.
*   `wait_for_elb_capacity`: Wait for Elastic Load Balancer capacity.

### `null_resource`

The `null_resource` resource waits for changes in the Autoscaling Group and triggers the `checkout.py` script.

*   `triggers`: Triggers for the null resource.
*   `provisioner "local-exec"`: Executes the `checkout.py` script with environment variables.

Cleanup
-------

To destroy the resources created by Terraform, run:

`terraform destroy`

License
-------

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
