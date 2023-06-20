# DaNetwork-Testnet
HEADS UP!! For first time users of the terminal, a (linux) command is effected on the terminal by pressing the enter key after the commands. e.g to check the list of files in a directory, press `ls -l ` and then effect it by pressing the enter key and there you have the result . Thus, when you come by the word "run" for a particular command (in this gudide), press the enter key to effect the command .

This guideline (Step 1 - Step 3 ) applies for people using AWS ubuntu based EC2 instance. If you provisoned your instance using other cloud providers, please skip to step 4.

## STEP 1: Opening a Free Tier Personal Account with AWS

*N.B. Ensure to choose the basic free support tier*.

* Go to the AWS website: [AWS](https:// aws.amazon.com/free).

   
* Click on the "Create an AWS Account" button located at the top right corner of the page.


* You will be redirected to the account creation page. Fill in your email address and choose a password for your AWS account.


* Click on the "Continue" button to proceed.


* Provide your contact information and agree to the AWS Customer Agreement.


* Choose the "Personal" account type and click on the "Continue" button.


* Enter your personal information, including your name, address, and phone number.


* Review the details you have entered and make sure they are accurate.


* Provide your payment information. Note that AWS requires a valid credit card to create an account, even for the free tier.


* Once you have entered your payment information, click on the "Secure Submit/ Submit" button.


* AWS will perform some verification steps to confirm your identity and payment details.


* After the verification process is complete, you will receive a confirmation email with further instructions.

Congratulations! You have successfully created a free tier personal account with AWS.


## STEP 2: Provisioning an ubuntu-based EC2 instance for our workload.

* Log in to your AWS account

* On the top right corner of the homepage, change your region to N.Virginia {optional}

![Region](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/5b16568b-35e1-4227-853f-1fee8c6a0d46)

* On the top left corner of the console, locate the search bar and search for "EC2", Click on EC2. Locate the launch instance button and click on it.

![Launch instance](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/64052c42-9a67-4533-b3b9-e7513626e61d)

* In the instance creation page, name your instance anything you wish.

* Choose the Ubuntu AMI, and change from the default version 22.04 to 20.04 free tier eligible (just below the dafault 22.04 version)

![AMI page](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/cb7cae85-b2c9-4e78-8dab-b7f47760945c)

* Leave the instance type as t2 micro free tier eligible.

* In the key pair section, click on the create new key pair button, give your key pair a name, and proceed to create.
  
Note the folder ( on your pc ) wherein the key pair is downloaded to (usually in the downloads folder).

![key pair 1](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/2cb8fd84-c60a-4c47-b946-64f5d2b0649b)

![Key pair 2](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/3e3abdb3-16a1-41e0-b74a-8adf962d0564)

* In the network settings section, click on the edit button and scroll down the page. Keep TCP 30301 (OR 30300-30400) and UDP 30301 (OR 30300-30400)open for the outiside world so that other nodes can discover your node.

![SG 1](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/b158aec8-4575-467b-ac29-9c4857d84ab1)

![SG 2](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/c97b812a-7a61-4344-bc19-51eeaccd2616)

* In the configure storage section, click on add volumes and provision an additional 20GB EBS volume.

![configure storage](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/aacad8bf-a0c6-4639-968e-4fcc3426b35c)

* Navigate to the base of the screen and click on the "Launch Instance" button. To access the created instance, click on the ID of the instance generated

  Subsequently,you can view your instance in the "instances (running)" section of the EC2 resource dashboard.

## STEP 3: SSH LOGIN INTO THE CREATED EC2 INSTANCE

* Select the instance created, and click on the "connect" button right on top.

![Click and connect](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/d3e13999-ed20-42c4-a2ab-fbe5ae71d121)

* Select the "ssh client" mode of connection and copy the ssh syntax provided as an example close to the base of the page. We shall use this syntax to log in to our instance right from the terminal.

![ssh client and ssh login syntax](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/7c951e35-4340-4bcf-8ea9-a5cb10942e98)

* Locate windows powershell through the seacrh bar on your windows page and open it. For mac users, locate your terminal.

* Depending on the location wherein the key pair was downloaded, change directory therein and paste the syntax we copied earlier.

  Mine was downloaded in the "Downloads" folder. Enter the folder by running ` cd Downloads `. Afterwards, paste the syntax you copied.

![TERMINAL LOGIN](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/ab97da7b-d634-4ab6-bf3b-6f8b25386305)

* Reply "yes" to the prompt and press the enter key. We have successfully ssh into our instance.


## STEP 4: TESTNET

* Visit the testnet documentation page on Github; {DaNetwork}(https://github.com/DaNetworkTech/TestNet)

* Clone the github page to your current working directory; ` git clone https://github.com/DaNetworkTech/TestNet `

* Navigate to the TestNet directory by running ` cd TestNet ` and make the danetwork-linux-amd64 binary executable by running: ` chmod u+x danetwork-linux-amd64 `

* Create an account for Node using the password: nodepwd1 by running the command ` ./danetwork-linux-amd64 --config node.toml account new `

  This prompts you to input passowrd. Input nodepwd1, press enter, type the password anew, and press the enter key. 

N.B: A contract address will be generated. Copy it and have it saved somewhere.

* Create a file "node.pwd" containing the password "nodepwd1" by running ` echo "nodepwd1" > node.pwd `. To check if your file was successfully created, run `ls -l `. To check the content, run ` cat node.pwd `.

  We shall use the contract address generated earlier and the password file "node.pwd" right away in our "node.toml" configuration file. 

* Open the "node.toml" file with a text editor by running ` nano node.toml `. (Use the arrow keys to navigate)

* Uncomment the engine_signer and password in the mining and account section respectively (This is done by deleting the preceding "#" symbol). 

* Supply the contract address that you saved as a value to  "engine_signer" in the [mining] section and the password file in the [account] section. An example is presented below;

```
[account]
password = ["node.pwd"]

[mining]
engine_signer = "0xc974716fbfd96dea9327a4dd7b4d0262e0a4cde5"
reseal_on_txs = "none"
force_sealing = true

```

![TOML](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/78644eb1-dee3-4f9b-83aa-23d0b2a552c5)

* Save the file with "ctrl O" (Control and letter O keys), click enter, and press "ctrl x" to exit the file. 
  
  To validate if your changes were effected, run ` cat node.toml ` command.

* Run the test chain using the node.toml configuration file as a parameter. To start the test chain, enter the following command in the command line: ` nohup ./danetwork-linux-amd64 --config node.toml & `. Press the enter key to secure your terminal

N.B: The "nohup" and "&" added at the begnning and the end of the command respectively helps us to run our mining process in the background with the output directed to a "nohup.out" file which is saved in your current TestNet directory(run ` ls -l ` command to confirm this). This ensures that the terminal is not hijacked by the running process and you can do other things on the terminal while the mining runs in the background.

How do you minitor the mining process???

* Run the ` tail -f nohup.out ` command to view a real time output of your mining process. To exit the file, press "ctrl c".

![tail command](https://github.com/Babbexx-22/ProjectBasedLearning/assets/114196715/f3f08aa4-63fd-42dd-b7b1-38ac887448c0)

## HAPPY MINING!!!
