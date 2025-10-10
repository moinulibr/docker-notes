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



এই প্রজেক্টটি স্থানীয় ডেভেলপমেন্ট পরিবেশের জন্য Docker এবং Laravel Sail ব্যবহার করে কনফিগার করা হয়েছে। এই গাইডটি অনুসরণ করে আপনার মেশিনে দ্রুত প্রজেক্টটি চালু করুন।

🛠️ সেটআপ গাইড (Setup Guide)
১. ডকার কেন ব্যবহার করব? (Why Docker?)
এই প্রজেক্টে ডকার ব্যবহার করার প্রধান কারণ হলো পরিবেশের সামঞ্জস্য (Environment Consistency) নিশ্চিত করা। এর ফলে, সকল ডেভেলপারের মেশিনে এবং লাইভ সার্ভারে সফটওয়্যার ভার্সন (যেমন PHP, MySQL) হুবহু একই থাকে, যা কোড কনফ্লিক্ট বা "আমার মেশিনে চলছে" ধরনের সমস্যা এড়াতে সাহায্য করে।

বিষয়

Laragon/XAMPP (ভার্সন কনফ্লিক্ট)

Docker (কন্টেইনার)

পরিবেশ

সিস্টেমের সাথে সরাসরি ইনস্টল হয়, ভার্সন পরিবর্তন হতে পারে।

বিচ্ছিন্ন কন্টেইনারে চলে, সব জায়গায় একই ভার্সন।

সিস্টেম পরিচ্ছন্নতা

আপনার লোকাল সিস্টেমে সরাসরি ফাইল এবং কনফিগারেশন যোগ হয়।

কোনো পরিবর্তন ছাড়াই বিচ্ছিন্ন পরিবেশে কাজ করে।

দলগত কাজ

Git-এ প্রজেক্ট ক্লোন করে দ্রুত অভিন্ন পরিবেশ তৈরি করা যায়।

Git-এ কমিট করা ডকার ফাইল ব্যবহার করে পুরো টিম একই পরিবেশে কাজ করতে পারে।

২. উইন্ডোজে ডকার ইনস্টল (Windows Setup - Mandatory)
উইন্ডোজে ডকার ডেস্কটপ চালানোর জন্য WSL 2 (Windows Subsystem for Linux 2) থাকা বাধ্যতামূলক।

ধাপ

কাজের বিবরণ

কমান্ড

২.১. WSL 2 ইনস্টল

PowerShell অ্যাডমিনিস্ট্রেটর হিসেবে চালু করুন।

wsl --install

২.২. রিস্টার্ট

কম্পিউটারটি রিস্টার্ট করুন।

(Manual Restart)

২.৩. Docker Desktop ইনস্টল

অফিশিয়াল ওয়েবসাইট থেকে Docker Desktop for Windows ডাউনলোড করে ইনস্টল করুন। ইনস্টলেশনের সময় 'Use WSL 2 based engine' অপশনটি চেক করা নিশ্চিত করুন।

(Installer Run)

২.৪. ডকার চালু

Docker Desktop চালু করুন এবং সিস্টেম ট্রেতে "Running" (সবুজ) স্টেট না দেখা পর্যন্ত অপেক্ষা করুন।

(Manual Launch)

🚀 প্রজেক্ট চালু ও কমান্ড (Running the Project)
প্রজেক্টটি Laravel Sail ব্যবহার করে কনফিগার করা হয়েছে।

ধাপ ১: কন্টেইনার চালু
প্রজেক্টের রুট ডিরেক্টরিতে টার্মিনাল খুলে নিচের কমান্ডটি দিন:

./vendor/bin/sail up -d

sail up: docker-compose.yml ফাইল অনুযায়ী সব প্রয়োজনীয় সার্ভিস (PHP, MySQL) চালু করে।

-d: Detached Mode এ ব্যাকগ্রাউন্ডে কন্টেইনারগুলি চালু রাখে।

⚠️ দ্রষ্টব্য: প্রথমবার চালানোর সময় ইন্টারনেট থেকে ইমেজ ডাউনলোড হবে, তাই কিছুটা সময় লাগতে পারে।

ধাপ ২: প্রয়োজনীয় কমান্ড চালানো
ডকার এনভায়রনমেন্টে থাকার কারণে, সব কমান্ডের আগে ./vendor/bin/sail যুক্ত করতে হবে।

স্ট্যান্ডার্ড কমান্ড

ডকার/সেল কমান্ড (প্রজেক্টের রুটে)

composer install

./vendor/bin/sail composer install

php artisan migrate

./vendor/bin/sail artisan migrate

npm run dev

./vendor/bin/sail npm run dev

php artisan test

./vendor/bin/sail artisan test

ধাপ ৩: অ্যাপ্লিকেশন অ্যাক্সেস
কন্টেইনার চালু হওয়ার পর ব্রাউজারে নিচের ঠিকানায় প্রজেক্টটি দেখুন:

http://localhost

ধাপ ৪: কাজ শেষে বন্ধ করা
সিস্টেম রিসোর্স বাঁচাতে কাজ শেষ হলে কন্টেইনারগুলি বন্ধ করুন:

./vendor/bin/sail down

sail down: চালু থাকা সব কন্টেইনার বন্ধ করে দেয় এবং সরিয়ে ফেলে।