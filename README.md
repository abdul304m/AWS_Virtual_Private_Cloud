# AWS_Virtual_Private_Cloud 

# what is  VPC (Virtual Private Cloud)?
A VPC is your own private network inside AWS.

- Think of it as your own isolated data center.

- You define how networking works: IP ranges, subnets, gateways, etc.

- Default VPCs are created by AWS, but you can create custom ones.

# Subnet:
A subnet is a smaller segment inside a VPC.

- You break a VPC into subnets for organization and control.

## Types:
- Public subnet → can access the internet.
- Private subnet → cannot access internet directly.

#  Internet Gateway (IGW)
An Internet Gateway lets your VPC talk to the internet.

- Required for EC2s in public subnets to be accessible from the internet.

- Must be attached to the VPC and referenced in the route table.

#  NAT Gateway
A NAT Gateway allows instances in a private subnet to access the internet (for updates, downloads, etc.) — but they cannot be accessed from the internet.

- NAT = Network Address Translation.

- Placed in a public subnet, and referenced in the private subnet’s route table.

#  IP Address
An IP address is a unique number identifying a device on a network.

# Types:

- Public IP: Reachable over the internet.

- Private IP: Only reachable inside the VPC/local network.

# CIDR (Classless Inter-Domain Routing)
CIDR defines IP address blocks.

#  Gateway
A gateway is a connection point between networks

# Types
- Internet Gateway: Connects VPC to internet.

- NAT Gateway: Allows private subnet outbound internet access.

- Virtual Private Gateway: For connecting to on-premises networks (via VPN).

# Route Table
A route table tells traffic where to go.

Each subnet in your VPC uses one route table.
Contains rules like:

- 10.0.0.0/16 → local (stay within VPC)

- 0.0.0.0/0 → igw-abc123 (send internet traffic to internet gateway)

- 0.0.0.0/0 → nat-xyz456 (send internet traffic from private subnet to NAT)

#  Connection Between Route Table & Gateway
This is how AWS knows how traffic should flow:

1. If you want internet access:

- Attach an Internet Gateway to the VPC.

- Edit the route table to send 0.0.0.0/0 traffic to that gateway.

2. If you want private instances to reach internet:

- Set up a NAT Gateway in a public subnet.

- Update private subnet's route table to send 0.0.0.0/0 → NAT Gateway.

# Setting up VPC

# PART 1
1. Naviagte to the search bar
a. Search for VPC and click on it , it wil direct you to the virtual pivate cloud.
![vpc](./New-pic-18/1.vpc.png).

2. Naviagte to the create vpc option and click on it.
![create-vpc](./New-pic-18/2.create%20vpc.png).

3. select the 'vpc' only option, specify the IPV4 CIDR block and proceed by clicking on proceed.
![set-vpc](./New-pic-18/3.set-vpc.png).

Your vpc was created successfully.
![created](./New-pic-18/4.vpc-created-succ.png).

# PART 2.
1. Navigate to the subnets and click on create subnets
![create-subnets](./New-pic-18/5.create-subnet.png).

2. select the ID of the vpc you created in part 1
![select-subnets](./New-pic-18/6.select-the-vpc-created.png).

3. Now enter the subnet name , and specify the IPV4 CIDR for the subnets , choose the availability zone.
![set-subnets](./New-pic-18/7.set-subnets.png).

a. click on add subnets to create another subnets.
![click-on-add](./New-pic-18/8.click-create.png).

b. Repeat the same steps fo the second subnets.Once completed click on create .
![second-subnets](./New-pic-18/9.secon-subnet.png).

Here you will see your subnets is being created.
![subnets-created](./New-pic-18/10.subnets-created.png).


# PART 3.
1. click on the internet Gateway option on the left sidebar and click create.
![inernet-Gateway](./New-pic-18/11.internet-gateway.png) .

2. provide the name for the internet Gateway and click create.
![name-the-internet-gw](./New-pic-18/12.name-it.png).

Now your internet Gateway has been successfully created 
![created-successfully](./New-pic-18/13.created-succ.png).

To enable internet connectivity , you must attach the internet gateway to the vpc you have previously created .

Now , attach it
![attach-vpc](./New-pic-18/14.attach-vpc.png).

![select-to-attach](./New-pic-18/15.select-to-attach.png).

![successfully-attached](./New-pic-18/16.successfully-attach.png).

# PART 4.
1. Procedd to the route table option and create the route table 
![route-table](./New-pic-18/17.Route-table.png)

2. provide a name of the route table and select the vpc you created previously. and click on route table .
![naming-route](./New-pic-18/18.Nmaing-route.png).

Now your route table has been crated .
![route-created](./New-pic-18/19.route-created.png).

a. To associate the route table with subnets, click on subnet association. followed by edit subnet association. we will assiciate the public subnet with this route table .
![subnet-association](./New-pic-18/20.subnet-assocition.png).

3. choose the public subnets and click on save association.
![choose-subnets](./New-pic-18/21.choose-subnt.png).

4. Navigate to route and click on Eddit route.
![navigate-to-route](./New-pic-18/22.navigate-to-route.png).

5. click on add route.
![setting-route](./New-pic-18/Add-route.png).

6. select Destination 0.0.0.0/0 indicatong that every IPV4 address can access this subnets.

7. In the target field , choose internet gateway and then select the internet gateway you created and clik on save changes .
![setting-route](./New-pic-18/23.setting-route.png).

The route table has now been configured to route traffic to the internet gateway  , allowing connectivity to the internet . since only the subnets named my-public-subnet-1 is associated with this route table . therefore only resources within that subnet can access the internet .
![route-configured](./New-pic-18/route-configured.png) .


# PART 5.
1. Navigate to the NAT Gateways setion and click on create .
![NAT-Gateway](./New-pic-18/24.NAT-Gateway.png)

2. privide a name of the NAT gateways.choose the private subnets, select connectivity type as private.click on create NAT Gateway
![Set-NAT-Gateway](./New-pic-18/25.set-gatway.png)

3. Your NAT Gateway is being created successfully.
![created-NAT](./New-pic-18/26.created-NAT.png).

4. Select your NAT Gateway. Navigate to the Details Tab, locate subnet ID and click on it.
![select-NAT](./New-pic-18/27.select-NAT-Gateway.png).

5. In the subnet page navigate to the Route Table setion.
![select-route-table](./New-pic-18/28.select-route-table.png).

6. proceed to route section and click on edit route.
![route-section](./New-pic-18/29.route-section.png).

7. click Add route.select Destination as 0.0.0.0/0, choose NAT Gateway in the Target field. then select the NAT Gateway you created and click save changes .

![add-route](./New-pic-18/30.Add-route.png).

8. On the subnet association section , click on edit subnet association.
![subnet-association](./New-pic-18/31.subnet-association.png).

a. choose the private subnet ansd click on save association.
![choose-private-subnets](./New-pic-18/32.choose-private.png).

Now  that the subnet has been successfully attached with the route table.
![subnet-updated](./New-pic-18/33.subnet-updated.png) .

# Differences Between Internet Gateway and NAT Gateway.
INTERNET GATEWAY:
- Allows instances in a public subnet to access the internet and receive traffic from the internet
- Inbound & Outbound internet traffic

NAT GATEWAY:
- Allows instances in a private subnet to access the internet, but prevents incoming traffic from the internet
- Outbound only (from private subnet to internet)

#  What is VPC Peering?
VPC Peering is a networking connection between two Virtual Private Clouds (VPCs) in AWS that allows instances in both VPCs to communicate with each other as if they are on the same network.

#  Why Use VPC Peering
- Your app is split into multiple services in different VPCs — they need to talk to each other.
- You're using separate AWS accounts for dev, test, and prod — peering allows communication between their VPCs.
- Centralized services (like logging, monitoring, AD, DNS) in one VPC, accessed by others.
- Need to share data between teams or projects securely, without exposing it to the internet.

# PRACTICAL PART.

## PART 6.
1.Lets begin by creating two VPCs in the same region. Alternatively, you may choose a different region if you needed.
![requester-vpc](./New-pic-18/34.requester-vpc.png)

![accepter-vpc](./New-pic-18/35.acceptr-vpc.png).

2. Navigate to the peering connection option . click on it and go create peering connection.
![peering-connection](./New-pic-18/36.peering-connection.png).

3. provide name for the peering connection vpc
a. select requester vpc 
b. choose tge account 'my account' since the vpc are in our aws account.
c. ensure to use  the same region 
d. select the accepter vpc
e. proceed by clicking on create peering connection button. 
![vpc-peering](./New-pic-18/37.vpc--peering.png).

![click-create](./New-pic-18/38.click-create.png).

Then , you will see this 
![created-successfully](./New-pic-18/39.created-successfuly.png).

4. locate the action option and click on it , then select accept request.
![locate-Action](./New-pic-18/40.locate-Action.png)

![Accept-request](./New-pic-18/41.accept-request.png).

![accepted](./New-pic-18/42.accepted.png).

5. Now click on main route table ID of the accepter VPC.

6. Choose route table and navigate to the route section, and click on edit route.
![route-table](./New-pic-18/43.rout-table.png).

a. click on add route.
![add-route](./New-pic-18/44.add-route.png).

7. Go to VPC page. select requester vpc . in the detail tab , find and copy IPV4 CIDR and pase it in the Destination field when adding route.
![ipv4-cidr](./New-pic-18/45.IPV4-CIDR.png).

a. In the target , choose vpc peering and choose the peering connection you have created and click on save changes.
![choose-peering](./New-pic-18/Choose-peering.png)

8. Now , copy the IPV4 CIDR of the accepter vpc
![ipv4-accepter](./New-pic-18/46.ipv4-accepter.png)

9. Now click on main route table ID of the requester

10. choose a route table , then navigate to the route section. click on edit route. 
![choose-route](./New-pic-18/47.choose=rout-table.png).

11. click on add route
![add-route](./New-pic-18/48.add-route.png).

a. paste CIDR in the destination field, in the target choose vpc peering and choose the peering connection you created.
![set-peering](./New-pic-18/49.set-peering.png).

The connection has been successfully established . Now, resources in the accepter vpc can connect to resources in the requester vpc and vice versa.
