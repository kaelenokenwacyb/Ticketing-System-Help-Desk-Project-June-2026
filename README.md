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

<img width="1109" height="617" alt="image" src="https://github.com/user-attachments/assets/630c7957-87b4-4d74-9c54-27514790656d" />

After verifying that Docker was installed, the next step was to create my osticket-lab folder, which is what would be used as the central workspace and root directory for the ticketing system. To do so, once again within PowerShell, I manually decided to create the file rather than doing it the conventional way, just because this method lined up better with staying consistent with the .env file creation (coming right after). To create this file, I ran the script below based on my Desktop's file path so that the folder could be made.

<img width="817" height="264" alt="image" src="https://github.com/user-attachments/assets/b704dd95-e67d-49d0-914b-e903315f0c5b" />

With my osticket-lab folder made and showing on my desktop, the next step was to create my .env file (environment file). By running this script within PowerShell, the .env file was made, allowing for credentials to be stored for osTicket, and for these credentials to be entered into my containers through Docker so that osTicket could successfully access the MySQL database.

<img width="532" height="155" alt="image" src="https://github.com/user-attachments/assets/6f48d4c0-1462-424d-93ac-7e2020944f7c" />

Finally, having completed the setup for my onticket-lab folder and my .env file, I was ready to create the final file needed, which was the docker-compose.yml file. This file acts as a type of blueprint for the entire architecture of my lab. It makes external acces rules for port mapping, creates dependencies for start up orders within the lab, and also gives Docker notice to create a dedicated storage space on my computer's hard drive so that my tickets and settings can be saved locally rather than disappearing once the lab is turned off. Once I entered the script for this file, the necessary containers were ready to go and I was prepared to begin using Docker.

<img width="1099" height="585" alt="image" src="https://github.com/user-attachments/assets/b9411df4-9d08-40a0-82ed-a08e3cd5f485" />
<img width="1101" height="174" alt="image" src="https://github.com/user-attachments/assets/a9be3477-16b3-4174-97fb-926a4952e88d" />

## Accessing osTickets
Now that my containers were ready to go, I was now able to start using osTicket with the help of Docker. On my internet browser, I typed in http://localhost:8080 to access osTicket, bringing me to the Support Center homepage. From here, I was shown various options, from being able to open a new ticket, to checking ticket status, and more. This is the screen that employees typically see when they wish to make a new request based on the problems they're facing within their environment.

<img width="1365" height="709" alt="image" src="https://github.com/user-attachments/assets/92a16ee7-335f-42f3-8f6e-2ce623926de0" />

Now that I was sure that this screen was working, I decided to access the Admin Page next (http://localhost:8080/scp/login.php). This page also worked successfully, and prompted me to login with the ostTicket credentials default to this simulation. After doing so, I was brought to the page in which I could see any tickets sent to me (the admin).

<img width="1365" height="717" alt="image" src="https://github.com/user-attachments/assets/c3e9b44f-4de3-4932-9351-b5fa2bde5b2e" />

## Admin Side Ticketing

Now that both pages were working successfully, it was time to test out actually sending a ticket and testing to see if I could view it from the admin page. Back on the ticket submission page, I pressed "Open a New Ticket" and filled out the form with the credentials that I wanted to be used. I used many placeholder credentials, as I simply wanted to see whether or not this would work. Some of the fields involved in this process were of course email, phone number, help topic, subject, and message, allowing the end user to supply the admin with all information necessary for a solution to be found.

<img width="1365" height="719" alt="image" src="https://github.com/user-attachments/assets/f07f1a5e-c656-4ab6-bfbe-0920c1c5ce5a" />
<img width="1365" height="715" alt="image" src="https://github.com/user-attachments/assets/3ed80238-8a7a-47bd-86b8-16172b53ad59" />
<img width="1365" height="720" alt="image" src="https://github.com/user-attachments/assets/847601cf-7d79-4990-b251-fd6b49a4bc3d" />

After submitting the ticket, I switched back over to the admin side and could successfully see the ticket that was previously submitted.

<img width="1365" height="715" alt="image" src="https://github.com/user-attachments/assets/f788ec6e-9b20-41ff-9562-a1e4afcbb071" />

Next up, I tested out actually responding to a ticket. I had many options, from choosing exactly who to respond to, typing out my response message, and being able to add a signature, add files, and also update the ticket status. For this practice example, I typed a simple response and posted the reply for the end user to see.

<img width="1365" height="715" alt="image" src="https://github.com/user-attachments/assets/68f40f59-505b-449e-9e9b-bc1ab76316a1" />

The step step of this process would now be creating and solving simulated ticket requests as a way to practice both being able to resolve tickets, and complete actual solutions through Active Directory.








