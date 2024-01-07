Streamlining Cloud-Based Deployment: A Beginner’s Guide to Dockerizing and Deploying Applications




In today’s dynamic digital landscape, deploying applications efficiently is a critical aspect of software development. Docker, an innovative containerization technology, simplifies this process by enabling seamless deployment across various environments. In this article, we’ll walk through the step-by-step process of installing and configuring Docker Engine, creating a Docker image, running a container, and uploading the image to Docker Hub, all while utilizing an EC2 instance via Session Manager.

Using CloudFormation to create our Ec2 (with predownloaded files)
Use the following link to create the EC2 instance click.

As you commence, remember to acknowledge CloudFormation’s potential requirement for creating IAM Roles for your stack.

![Screenshot 2024-01-02 165943](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/225e679c-eb0a-414e-893e-9ecf75ae8012)


Once your stack is completed, go to the EC2 UI and ensure you have a new running instance.

![Screenshot 2024-01-02 172254](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/400cdfc3-6fb7-40f9-8f1a-ac0c15b08491)


Installing Docker Images on EC2
The next step involves a seamless connection to the instance using Session Manager.
![Screenshot 2024-01-02 172332](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/31dc9d88-b884-4212-822f-d3ea2a5ca801)

Now, the stage is set for the installation of Docker image packages, enabling the magic of Docker to unfurl on this EC2 instance. Execute the following command to initiate the installation process:

Hint: Utilize sudo for administrative privileges and dnf as your trusty package manager.

sudo dnf install docker
As you proceed, an affirmative ‘y’ will be your nod of approval when prompted to verify the package installation.

![Screenshot 2024-01-02 172759](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/976242cf-b858-4299-9856-036541f42407)

Upon completion, breathe life into the Docker service with a simple command:

sudo service docker start

![Screenshot 2024-01-02 172610b](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/bd13e8e1-7c14-4b55-a7df-8aca8845f4d1)


However, at this juncture, our user lacks the interaction prowess with Docker on this EC2 instance. Fear not, grant access to any user on this instance to wield Docker’s might with the following command:
![Screenshot 2024-01-02 173034](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/689c7733-dc95-4358-9435-f3091ac4a154)

sudo usermod -a -G docker ec2-user
Hint: usermod - the key to modifying group privileges for a root user.

After a brief exit from the instance through Session Manager and a swift return, use the command below to immerse yourself into the EC2 instance as a user:

sudo su - ec2-user
With this command, you’ve successfully entered the realm of the instance as a user. Verify Docker functionality with a simple:

docker ps

![Screenshot 2024-01-02 173234](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/6a94d493-d4aa-4e9e-8b90-30b7f4d94d9e)


If you use the command ls, you will see the instance was configured. To download the sample application, we will be using (that is what the file, container.zip, is). The instance was configured to extract the zip file into the container folder, as seen below.

![Screenshot 2024-01-02 174042b](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/23e8ad94-13b7-4e07-9192-41be76063ec5)

Next, change directories into the container by using the following command:

cd container
Next, use the command ls -l. This command will show you the web application files (Docker files) that the EC2 downloaded.

![Screenshot 2024-01-02 174042c](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/0320f150-424c-42c9-97a3-d7207fec6d10)

Now, let’s take a look at the Docker file downloaded onto our EC2 instance, unraveling its cryptic contents:

![Screenshot 2024-01-02 195904](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/aaa13ae6-33ec-42ae-b84b-6dda55eafdbe)

From: Tells us we want to use a base image and a certain version. As you see, `redhat/ubi8` is an image and version.

Label: A placeholder (description of the image).

Run: As it says, it runs a command, in this case, a `yum` command to install software.

Copy: Copies files from the local directory and into your Docker file when you create an image.

Copy (second copy): Does the same process but for all the jpg files in the folder.

Entry point: Sets the entry point and determines what is first run when this image is used to create a Docker container.
Expose: Used for a Docker image to know which port is exposed.
Build container image.

Build the container.
Now that we have a sound understanding of our Docker file/image, it is now time to create our container. Do so by using the following command:

docker build -t containerofcats .
Hint: the . at the end contains the working directory for the Docker file and files associated with the Docker file. The container should run through every line, performing each directive, and each directive is going to create another layer within the Docker image.

![Screenshot 2024-01-02 174042](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/16835b89-6cad-450c-95bc-38daa1671262)

Now, we view the Docker image we just created by using the following command:

docker images --filter reference=containerofcats
Now we will run our container by using the following command:

docker run -t -i -p 80:80 containerofcats
Hint: 80:80 - we are telling our container to map port 80 on the container with port 80 on the EC2 instance.

![Screenshot 2024-01-02 174421](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/992ff10d-815a-4084-862a-bbcabae07c74)

To ensure our container is running on our EC2 Instance, we will check our public IP address. Return to the EC2 Console and copy the public IP Address.

Next, place the address in a new tab and see if our container is running.

![Screenshot 2024-01-02 174316](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/bafb9f55-08c9-41a6-9583-72eb57e33569)

Congratulation! You are becoming an Docker Experts!
Wait, But There’s More!
Now we will upload our container to Docker Hub. Yes, we will keep our container on Docker Hub from the EC2 Instance.

Use ‘control + C’ to exit the running container. Then use the following command to log into Docker Hub. Replace ‘YOUR_USER’ with your Docker Hub username. Next, you will be prompted to enter your password. Don’t worry about the ‘unencrypted password warning’; we will delete the EC2 after uploading our container.

docker login --username=YOUR_USER

![Screenshot 2024-01-02 175208b](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/b92ea28a-85ae-4cbb-98ee-eb5ee30aaddb)


Once you’re successfully logged in, use the following command to view your images:

docker images
Copy the image ID of the image you want to push to Docker Hub (in our case, “containerofcats”). Use the following command to tag your image, replacing ‘YOUR_USER’ with your username for Docker Hub:

docker tag IMAGEID YOUR_USER/containerofcats

![Screenshot 2024-01-02 175208c](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/a2453a38-067b-4dcf-846d-6cc0e00f4083)

Now use the following command to push your image to Docker Hub, again replacing ‘YOUR_USER’ with your username for Docker Hub:

docker push YOUR_USER/containerofcats:latest

![Screenshot 2024-01-02 175208](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/6d9be32d-d79d-42a0-b971-8c450bdac99e)

Sign into Docker and ensure your image has successfully made it to your account.

![Screenshot 2024-01-02 175330](https://github.com/jd-turner/aws-vpc-flowlogs/assets/129380235/5969a253-f131-49d1-95df-0229a9a52b82)

Now that your image is in your Docker account, you can now pull images from there into Virtual Machines.

The Endless World of Containers.
In closing, this journey into Docker’s realm, orchestrated atop an EC2 instance through CloudFormation’s orchestration, serves as a stepping stone to a world of innovation. Armed with newfound insights, you now possess the keys to unlock boundless possibilities within containerization. The horizon beckons — keep exploring, keep creating, and keep shaping the future of container-based applications. Thank you for time.
