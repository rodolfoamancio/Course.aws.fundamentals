# Amazon EC2 autoscaling

First, it is necessary to define a launch template, with name and description. Once again, it is necessary to set image, but in this case we point to the original instance. 

Following, it comes to network and other creation settings.

Then, to create a auto-scale group it is necessary to refer to the launch template previously created. And it is necessary to attach it to a load balancer. Additionally, we must define the desired capacity, along with minimum and maximum limits.

Next, we define the scaling policies. With `Target tracking scaling policy` we can choose the appropriate metric, target value and instances needs.
