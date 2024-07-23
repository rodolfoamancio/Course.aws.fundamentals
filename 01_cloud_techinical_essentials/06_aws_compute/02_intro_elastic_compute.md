# Introduction to Elastic Compute

Using the elastic compute infrastructure, you pay as you go, either by hour or second. To configure the computational cluster:
1. Select the desired `amazon machine image` (AMI): this will set the root volume template, with corresponding OS and pre-installed applications. Launch desired permissions and block device mapping.
2. It is possible to start multiple instances of the same image.
3. Start the instances, the names follows the pattern: `t3.medium`, `a1.large`. Where the first two letters before the point `.` are related to the instance type, while the latter word refers to the size of it. The size is related to the capacity the instance has, while the type refers to the blend of these resources.