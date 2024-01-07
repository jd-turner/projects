Welcome to a journey where we unveil the magic of AWS VPC Interface Endpoints! These are the secret passages that allow your AWS resources to connect seamlessly with your subnets, all while keeping things private. Today, we’re not just setting up infrastructure; we’re opening a door to a world of private connectivity wonders using CloudFormation.

Step 1: The Grand Entrance (Deployment)

Click your way to wonderland with this 1-Click Deployment. Name your stack — your AWS kingdom(infrastructure) in the making — and graciously acknowledge the CloudFormation IAM resources.

![1_PCmoRDzCYrzd2vnS5iBnPA](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/106abde7-f317-4d70-b2e7-4e0b824b1202)

Behold as the magic unfolds.

![1_DjFc7vEQaOc3Jr15nelHAg](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/9d38786c-0bd6-4ccf-aef2-c1566a0cdd31)

Step 2: Ensuring Secrecy (No Public IPV4)

Now, traverse to the EC2 console. Ensure that your created instance is devoid of a Public IPV4 address.
![1_mJgRW26wb1qPBtKnoejinw](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/89f7fe39-d809-44fc-a217-b8b90c916e8d)

With a nod to security, connect to the instance, selecting the EC2 instance connect option. Here, we weave the threads of secrecy.

![1_AHi3j8R0YnnnWeMjYQVZKA](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/6fa52ae6-8118-45a8-bcaf-a5288fddbd03)

Step 3: Creating the Endpoint

Select EC2 instance connect, and like a wizard conjuring a spell, create a new endpoint. Name it and select EC2 instance connect. Choose the right VPC, pick the security group, and designate the subnet, say sn-app-A. With a click, create the endpoint, and let the magic settle.

![1_P6VUTiIV4ma_kpX_5tEBbA](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/58d2b022-2613-4dfd-a0dc-70bad0af1095)

Wait for your interface endpoint to come alive.
![1_P6VUTiIV4ma_kpX_5tEBbA](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/58d2b022-2613-4dfd-a0dc-70bad0af1095)

Step 4: The Reveal (Test interface connection)

Return to the EC2 instances, connect again, selecting ‘Connect using EC2 Instance Connect Endpoint’. Connect your Endpoint by using the dropbox under ‘EC2 Instance Connect Endpoint’. As the digital curtain rises, revel in successfully logging into your instance.

![1_LXpHMAwA0v8c9S-i0TV_HQ](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/96658154-2ce0-4874-b1a4-47e9d7ed86d1)

Step 5: A Peek Behind the Curtain (Your Interface Endpoint Awaits)

Now, exit gracefully to log out, only to log back in with a hint of suspense. Witness the private IPV4 address for your interface endpoint, like discovering a well-guarded secret.
![1_XiGwFTyMz8w0P2aHGEdtPA](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/5116a3ae-e8eb-4828-9639-846b6db00656)

Step 6: Ensuring the Endpoint Is Connected

To add a final stroke to the enchantment, visit the VPC console. Click on endpoints and descend into the network interfaces of your endpoint. Click through the layers like a detective solving a mystery and confirm that your IPV4 PRIVATE ADDRESS matches the one elegantly connected to your EC2 instance.

![1_qcTd_bI2GlqZipWrQhOPyw](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/84e611f7-4c69-4c51-b4f0-d9d843ba1729)

Voila! With a few incantations and a dash of AWS magic, you’ve created an interface endpoint that dances in harmony with your EC2 instance. The magic is not just in the creation; it’s in the seamless connection that brings your AWS resources to life in the subnets, all hidden from the prying eyes of the digital realm. You’re not just configuring; you’re orchestrating a symphony of AWS wonder. Until next time friends!
