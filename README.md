# Ticketing-System-Help-Desk-Project
The objective of this lab is to architect and simulate an enterprise-grade help desk ticketing system mapped against a corporate organizational structure. Utilizing Docker for lightweight containerization and osTicket as the core service management platform, this project replicates the identical ticket-handling workflows utilized by modern IT support and security operations teams.  

To maximize the realism of this environment, I integrated this ticketing architecture directly with my Active Directory Home Lab. This allowed me to bridge the gap between service desk operations and system administration. Instead of just configuring the platform, I actively generated, triaged, and resolved simulated enterprise requests—such as account lockouts, onboarding workflows, and permission management—and documented the technical solutions directly within the platform. These are the various sections of this project:
- Introduction and Setup
- Accessing osTickets
- Admin Side Ticketing
- Solving Simulated Tickets

With this project, I hope that I'm able to use this experience in the real world, working to solve requests and isuses that people run into, not only with this ticket system experience, but with my overall troubleshooting and Active Directory experience as well.

# Environment Overview
- Personal Home PC (AMD Ryzen 5 3600, GTX 2070, 16GB RAM, 250GB SSD, 1TB HDD,...) built by myself (used to manage Active Directory Services)
- ASUS Vivobook Laptop (used to manage Docker + osTicket)
- Docker & Docker Compose (containerization and network isolation)
- osTicket (Service desk and ticket lifecycle management)
- MySQL (Persistent database backend)
- Active Directory (Identity administration and incident resolution)

# Skills Learned and Demonstrated
- Incident Response & Ticket Lifecycle Management
- Infrastructure Troubleshooting
- Identity & Access Management
- Security Auditing & Log Analysis
- Containerization & Service Orchestration

## Introduction and Setup
To begin with this lab, I first had to begin with setting up my two containers with Docker:
- Container #1 (osTicket)
- Container #2 (MySQL)

These two containers work to allow the ticket system to function over the Docker network that I set up. They are similar to virtual machines, in the sense of being able to turn them off and back on whenever needed for access.

The first step in this entire process, of course, was installing Docker. I downloaded the Docker Desktop software from the official website (https://www.docker.com/products/docker-desktop/). I decided to use my ASUS Vivobook for all Docker and osTicket processes rather than my Home PC so that I could dedicate each device to one thing. After having downloaded Docker, I entered my PowerShell to ensure the proper version was added to my system. 

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/630c7957-87b4-4d74-9c54-27514790656d" />

After verifying that Docker was installed, the next step was to create my osticket-lab folder, which is what would be used as the central workspace and root directory for the ticketing system. To do so, once again within PowerShell, I manually decided to create the file rather than doing it the conventional way, just because this method lined up better with staying consistent with the .env file creation (coming right after). To create this file, I ran the script below based on my Desktop's file path so that the folder could be made.

<img width="850" height="400" alt="image" src="https://github.com/user-attachments/assets/b704dd95-e67d-49d0-914b-e903315f0c5b" />

With my osticket-lab folder made and showing on my desktop, the next step was to create my .env file (environment file). By running this script within PowerShell, the .env file was made, allowing for credentials to be stored for osTicket, and for these credentials to be entered into my containers through Docker so that osTicket could successfully access the MySQL database.

<img width="550" height="400" alt="image" src="https://github.com/user-attachments/assets/6f48d4c0-1462-424d-93ac-7e2020944f7c" />

Finally, having completed the setup for my onticket-lab folder and my .env file, I was ready to create the final file needed, which was the docker-compose.yml file. This file acts as a type of blueprint for the entire architecture of my lab. It makes external acces rules for port mapping, creates dependencies for start up orders within the lab, and also gives Docker notice to create a dedicated storage space on my computer's hard drive so that my tickets and settings can be saved locally rather than disappearing once the lab is turned off. Once I entered the script for this file, the necessary containers were ready to go and I was prepared to begin using Docker.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/b9411df4-9d08-40a0-82ed-a08e3cd5f485" />
<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/a9be3477-16b3-4174-97fb-926a4952e88d" />

## Accessing osTickets
Now that my containers were ready to go, I was now able to start using osTicket with the help of Docker. On my internet browser, I typed in http://localhost:8080 to access osTicket, bringing me to the Support Center homepage. From here, I was shown various options, from being able to open a new ticket, to checking ticket status, and more. This is the screen that employees typically see when they wish to make a new request based on the problems they're facing within their environment.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/92a16ee7-335f-42f3-8f6e-2ce623926de0" />

Now that I was sure that this screen was working, I decided to access the Admin Page next (http://localhost:8080/scp/login.php). This page also worked successfully, and prompted me to login with the ostTicket credentials default to this simulation. After doing so, I was brought to the page in which I could see any tickets sent to me (the admin).

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/c3e9b44f-4de3-4932-9351-b5fa2bde5b2e" />

I could view tickets through various means, such as specifically viewing tickets that have been opened, or tickets that have been answered or are overdue. From this screen, I could also search for specific tickets, sort closed tickets based on the date they were closed, and many more useful features.

Extra: On this page, I could also see other features that most IT Support or Help Desk workers would deal with daily, such as being able to assign tickets to others and transfer tickets. These features are just as important as all other things covered in this lab, allowing the admin to be able to manage tickets with even more ease.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/b9fc71de-76ed-49b2-b3b5-d2750d2ef0bb" />
<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/f8c1ba88-b1da-4a06-b5d7-7baf07c11bc6" />

## Admin Side Ticketing

Now that both pages were working successfully, it was time to test out actually sending a ticket and testing to see if I could view it from the admin page. Back on the ticket submission page, I pressed "Open a New Ticket" and filled out the form with the credentials that I wanted to be used. I used many placeholder credentials, as I simply wanted to see whether or not this would work. Some of the fields involved in this process were of course email, phone number, help topic, subject, and message, allowing the end user to supply the admin with all information necessary for a solution to be found.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/f07f1a5e-c656-4ab6-bfbe-0920c1c5ce5a" />
<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/3ed80238-8a7a-47bd-86b8-16172b53ad59" />
<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/847601cf-7d79-4990-b251-fd6b49a4bc3d" />

After submitting the ticket, I switched back over to the admin side and could successfully see the ticket that was previously submitted.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/f788ec6e-9b20-41ff-9562-a1e4afcbb071" />

Next up, I tested out actually responding to a ticket. I had many options, from choosing exactly who to respond to, typing out my response message, and being able to add a signature, add files, and also update the ticket status. For this practice example, I typed a simple response and posted the reply for the end user to see.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/3b0a0ac9-d461-4770-93e5-73f6a66cbff6" />
<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/68f40f59-505b-449e-9e9b-bc1ab76316a1" />

The step step of this process would now be creating and solving simulated ticket requests as a way to practice both being able to resolve tickets, and complete actual solutions through Active Directory.

## Solving Simulated Tickets
For this section of the lab, I wanted to be able to test out both receiving tickets, solving them through Active Directory, and submitting a response back to the end user. Based on this, I used 4 made up scenarios to help me practice and gain experience:
- #1) User: Chris Redifield ; Issue: Account expired after expiration date passed, and user needs the date to be extended.
- #2) User: Tim Manager ; Issue: Onboarding for a new Network Analyst required me to create a new account for them, along with the proper sercurity group and temporary password.
- #3) User: Grace Ashcroft ; Issue: End user is unable to access their workstation as their account has been locked after too many incorrect password entries
- #4) User: Automated SIEM Alert ; Issue: High volume of failed login attempts has been noticed and must be analyzed

### Ticket #1: Account Expiration
For this first ticket, the user experienced their account expiring because the date set for the expiration had passed, but they had their contract with the company extended by 6 months. 

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/9044519a-e915-4a76-89f1-224e8c414522" />

To solve this, I used the User and Groups section of Active Directory / Server Manager to access the user's account.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/1209634d-0db5-4b23-aed9-493bad891131" />

Next up, I went to said user's properties, and to the account tab to view information on their account's expiration date. From here, I could see that their account was indeed set to expire (pretending that the date July 28th had passed based on this simulation). 

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/9c41494f-8a4b-4fb4-b8d2-9a59c192be2f" />

To remedy this, I set the new expiration date to be 6 months later (based on the employee's extended company contract), and hit apply so that the changes could take place.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/be74daa6-9f95-4de9-a3df-7be1aa56bcaf" />

With that being completed, I submitted a response to the user now that the root problem had been fixed.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/de9b8b8c-c189-4ff7-97ef-d8848dc3fa53" />

### Ticket #2: New Employee Onboarding
For the second ticket, a new Network Analyst was joining the company, and I had the responsibility of setting them up with a new account, along with the proper securtity group and temporary password set.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/3f6dd358-f6ed-4c56-842d-656c53297889" />

To solve this ticket, I had to use Active Directory's User and Groups tool to create a new user for the new employee. For this simulation, I placed this new user into the IT_Department Organizational Unit, and also created a new Organizational Unit within that one called 'Network_Analyst'. I then created a name and password that would be set to expire upon the next logon, forcing the new hire to create their own password to be used.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/18ec1a07-b1dc-486b-9eba-3df3dd99a038" />
<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/d4ad4d73-b23d-447a-8d50-f911dc27b9bc" />

Next up, I navigated to the Organizatinal Unit I had created, and selected New > New Group. Here is where I created a new security group (Network_Analyst) based on the new hire's onboarding process and permissions that he should have within his account. 

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/c3d08069-9df8-41c5-b186-b2f256591861" />

The final step was adding this new user to the security group, ensuring that his account was covered by the group.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/1f4840cd-cf2b-412f-887f-1f97eb9380ed" />

Finally, now that the requested ticket was completed, I sent a response back to the end user so that I could turn in the request.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/b3ffd7fa-c606-46c4-867e-1c073cdd2156" />

### Ticket #3: Locked Account
For this third ticket, the user was experiencing a locked account after accidentally inputting an incorrect password upon login. Within this ticket, time was of the essence, as this user had a presentation due in 20 minutes and no time to spare.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/35d82d4f-158d-4772-914a-37c7b751a5ff" />

For this ticket, I once again navigated to Users and Groups to find the user's name within the HR_Department Organizational Unit (from my Active Directory lab). 

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/c4cd646b-1705-4c57-8d1d-ab0d3f1b738c" />

From here, I was able to navigate to the user's properties through right-click, and checked the "Unlock account" button so that they could once again access their account. After doing so, simply pressing apply put the change into effect.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/1401c79f-d96b-4f58-85f9-933637c4a556" />
<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/d27966b8-2f8a-4cf9-b3ae-308736326d3c" />

With this ticket being completed, I sent in a response to the user to notify them of the fix.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/745bb947-0b64-4ef1-b170-3a2bb6a5ac64" />

### Ticket #4: Failed login attempts logged
Within this final ticket, I was tasked with analyzing the multiple failed attempts noticed by the company's security system. The system sent an alert in case the security was being breached, and I was tasked with looking through the audit logs to see what occurred.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/b782209c-ee84-4a4c-ac89-7f87b2b385f0" />

To solve this ticket, I navigated to Event Viewer on my server virtual machine, and filtered based on the ID 4625. This code signals that a logon attempt failed due to an incorrect password being used. 

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/398bd055-9774-4ea9-8aef-35ad81aa185c" />

After viewing the 4625 code, I was able to view the unsuccessful logon attempts. 

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/b27c0495-1ffe-4cdd-a7ff-68cc55f0fbac" />

I wanted to see if this was maybe a user that had accidentally entered their password incorrectly, so I then went on to view any successful attempts. I did the same process again, this time using the ID 4624 to view successful logon attempts.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/e3f5d9d7-6a98-4491-be9d-c7f5ab851330" />

From here, I could see that the user had successfully logged in eventually, but to make sure, I did still want to contact the end user for any concerns they may have had with their logon process (in an actual environment and ticket situation like this, I would of course make sure that the user DID indeed make these logon attempts and incorrect passwords before closing the ticket, just in case an outside individual was making the attempt to breach the systems). For the sake of this simulation, I pretended to have contacted the user to confirm their actions.

<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/d0f16046-95fa-443e-897d-e3ffc8ce5a69" />
<img width="850" height="600" alt="image" src="https://github.com/user-attachments/assets/d24d346e-db65-4bfc-850e-00c143d8276d" />

This marks the end of the ticket simulations.

## Conclusion
With these ticket simulations completed, I was able to not only gain experience using a ticketing system, but was also able to gain more Active Directory experience with being able to solve issues such as these. My hope is that in the future, I'm able to put this experience to practice in a real-world work environment, working to solve ticket requests for users and improve upon my Active Directory knowledge! As time passes, I will continue to further explore how I can use this ticketing simulation to learn even more about its capabilities, and continue to add onto this repository. Thank you for your time!














