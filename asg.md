# ASG

app VM  

   |

   |

   |

CPU load too high

|

|

Crash


app VM
  
  |
  
  |
  
  |

CloudWatch
Monitoring
(CPU Load)

  |

  |

  |

Dashboard----might miss it as we cannot observe it whole time

app VM

 |

 |

 |

CloudMonitoring
(CPU Load)

 |

 |

 |

Alarm

 |

 |

 |

Notification --- still requires alot of mannual work as we need to set up 

app VM

 |

 |

 |
Cloud Watch Monitoring
(CPU Load)

 |

 |

 |

Autoscaling--- solves those issues. 

### Why autoscaling is the best solution? 

In AWS autoscaling group helps scalability, high availability. 


**VM**---> we can copy the disk using AMI---> once AMI is set we can use lauch templete----------> This will be then help Autoscaling group as it needs to know the required details to create VMs. AS lauch templete will have all the required detailed such as NIC, NSG, image etc. 



### ASG

1.	Start db VM
2.	Created a new app VM using provision script
3.	Create AMI and then launch template using AMI.
4.	Test Launch template and then create ASG and Load balancer using DNS.

## How to Launch Template

1.	Go to Launch template on left hand side.
2.	Click on create launch template.
3.	Give name tech241-larisha-app-for-asg-LT
4.	Give template name---for first asg.
5.	Then go to launch template content, go to my AMI and select the image for asg-ami.
6.	Instance type
7.	Keypair name
8.	Network settings—SSH-HTTP-3000 app
9.	Advanced setting user data  add the app script just edited with only necessary steps.
10.	Select Launch template.
11.	Select Launch instance from template.
12.	Everything required should be all filled in and launch the template.


1.	Then select the instance and see the details.
2.	Then set up the tag before or manually name so it can be found.
3.	Name tech241-larisha-test-of-lt

## **ON Vscode copy the app provision script;
App provision only start app;**


**#! /bin/bash**

#echo “set environment variable”
**export DB_HOST=mongodb://:27017/posts**

#Cd into the app folder
**cd app2/app**

#Install npm

**npm install**

#Seed database

Echo “Clearing and seeding the database….”

**node seeds.seed.js**

#Start the app

**pm2 start app.**

# How to create ASG?

1.	Select ASG
2.	Select create ASG
3.	Give ASG name- tech241-larisha-app-asg
4.	Find the launch template you just made (tech241-larisha-app-for-asg-lt)
5.	Select next.
6.	Select the availability zone (Devops student default 1a, 1b, 1c)3 options. 
7.	Select next.
8.	Load balancing create a new load balancer.
9.	Select the type of load balancer Application load balancer
10.	Give name to load balancer tech241-larisha-app-asg-lb.
11.	Load balancer scheme internet facing.
12.	On listeners and routing add name target group—tech241-larisha-app-asg-lb-tg.
13.	Turn on the Health checks and select next.
14.	Select the group size 2, 2, 3
15.	Scaling policies target tracking scaling policy and select next.
16.	And next 
17.	Add tags, key(NAME) and value(tech241-larisha-app-asg-HA-SC).
18.	Select next and review and create ASG.
19.	Go to load balancer and go to details of your instance and copy the DNS name.
20.	Go to instances in another page.
21.	Find the instance associated with ASG (HA and SC) and select.
22.	Select the one from the bottom select and select instant state and terminate state.


# Remove the ASG 

1.	Go to load balancer and then select your load balancer.
2.	Select action and click on delete.
3.	Confirm.
4.	Go to ASG search for your asg and go on action and delete the asg. 

### The reason we must delete ASG else It will create a new instance even if you terminate. So, it is important to delete the ASG group. 
