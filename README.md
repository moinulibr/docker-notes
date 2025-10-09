Project Environment Setup Guide: Using Docker
This guide explains what Docker is, why we use it for local development, and how to set it up step-by-step on a Windows operating system to run your project.

1. What is Docker and Why We Use It
Docker is a platform that uses Containerization technology to package and distribute applications.

Simply put, Docker wraps your application and all its dependencies (like PHP, MySQL, Node.js) into a small, isolated package called a Container.

Why Docker Instead of XAMPP/Laragon?
We use Docker instead of traditional tools because it solves the core problem of "It works on my machine but not on yours."

Issue

Laragon/XAMPP (Version Conflict)

Docker (Container)

Environment Consistency

Your laptop has PHP 8.1, but the live server uses PHP 8.3. This can cause code breaks.

We define the container to use PHP 8.3. This container will behave identically on your machine, my machine, or the production server.

Clean System

Server software (like PHP and MySQL) is installed directly on your operating system.

The container runs in an isolated environment. It doesn't modify your Windows system settings or clutter your hard drive.

Teamwork

It's difficult to ensure every team member has the exact same local setup.

Docker files are committed to Git. Every team member can clone the project and run a single command (sail up) to get the identical, pre-configured environment.

2. Setting Up Docker on Windows (WSL 2)
To run Docker Desktop efficiently on Windows, WSL 2 (Windows Subsystem for Linux 2) integration is mandatory.

Step 1: Install and Prepare WSL 2
Launch PowerShell: Search for PowerShell in the Windows Start Menu and open it as "Run as Administrator."

Install WSL: Run the following command (this installs the Linux kernel and a default Ubuntu distribution):

wsl --install

Restart Computer: Restart your computer to apply the changes and ensure WSL 2 is properly loaded.

Verify Version (Optional): After restarting, run wsl -l -v to confirm your distributions are running on Version 2.

Step 2: Install Docker Desktop
Download: Download Docker Desktop for Windows from the official website.

Install: Run the .exe file. During installation, ensure the option 'Use WSL 2 based engine' is checked.

Launch Docker: Start the Docker Desktop application. Wait until the Docker icon in the system tray turns green or shows the "Running" status.

3. Launching the Laravel Project with Sail
We use Laravel Sail to manage the Docker containers for our project, as it simplifies the configuration using a convenient sail script.

Step 1: Start the Containers
Open your terminal (CMD/PowerShell/Git Bash) in the root directory of your project and run the following command:

./vendor/bin/sail up -d

sail up: Reads the docker-compose.yml file and builds/starts all required containers (PHP, MySQL, Node.js).

-d: Stands for Detached Mode. This runs the containers in the background, so your terminal remains free to accept new commands.

(The first time you run this, Docker will download the necessary images from the internet, which may take a few minutes.)

Step 2: Access the Application
Once the containers are successfully running, you can access the Laravel application in your web browser at:

http://localhost

Step 3: Running Project Commands
In the Dockerized environment, you can no longer use simple commands like php artisan or composer directly. You must use the ./vendor/bin/sail prefix to execute commands inside the correct container.

Standard Command

Docker/Sail Command

composer install

./vendor/bin/sail composer install

php artisan migrate

./vendor/bin/sail artisan migrate

npm run dev

./vendor/bin/sail npm run dev

Step 4: Stopping the Containers
When you are finished working, you should stop the containers to free up system resources.

./vendor/bin/sail down

sail down: Stops and removes all running containers related to the project.

4. Git Best Practices
Commit Docker Files: You must commit the docker-compose.yml file (and any custom Dockerfile if present) to Git. This ensures that every team member gets the identical environment blueprint.

Exclude Data: Ensure your .gitignore file contains entries for directories like vendor and your database file (database/database.sqlite). These files should not be committed.