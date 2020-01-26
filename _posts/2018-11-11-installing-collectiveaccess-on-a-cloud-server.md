---
layout: post
title: "Installing CollectiveAccess on a cloud server"
date: 2018-11-11
tags: [sysadmin]
---

I've worked with CollectiveAccess (an open source collections management system for galleries, libraries, archives, and museums, see website [here](https://collectiveaccess.org/)) on-and-off for around four years. I helped with the creation of digital backups and frontend design and development for the [LaMaMa Digital Archives](http://catalog.lamama.org/), a Dance Heritage Coalition project, and I have been working this year on the development of an archive (physical and digital, with me working on the digital preservation and access components) for the [Mark Morris Dance Group](https://markmorrisdancegroup.org/). When I came into the project, the system had already been installed on a local "server" (a Mac). There were some lingering configuration issues that manifested as bugs experienced by the users when doing cataloging work. Also, as the project grows and prepares to live a full life outside of the dance center's basement, we are now ready to move to what will eventually be a public access portal.

I'm going to go step-by-step through the things I did to install CollectiveAccess. This is the type of blog post that is basically me writing notes to my future self, in case I need to do this installation process again, and making these private notes public and more understandable, in case this helps anyone else going through the same process. Obviously some notes are redacted because they are for just me and the archives team.

Our project manager set up a Digital Ocean droplet and passed the credentials to me, and then I was ready to get crackin'.

Naturally, my first step was the start with the [official installation docs](https://docs.collectiveaccess.org/wiki/Installing_Providence). **Start here!** Everything you need to know is there, but it's not necessarily as friendly or intuitive as one would like it to be, so I had to do a lot of extra work in deciphering this documentation.

This instructions indicate that I need to essentially set up a LAMP stack. Digital Ocean provides great documentation on how to do this, and I also happen to be installing this onto Digital Ocean servers. [Here](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-16-04) are the docs, and I followed all of the steps listed here. This combines information found in their [MySQL installation docs](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-16-04), which I had started with.

In addition to all the PHP stuff installed in the above documentation, I also had to grab some modules/extensions. These are listed in the installation docs but it's not clear which are already installed by default, how to determine that information, or which ones were still necessary.

These were still necessary for separate installation, and the one-liner that will install them all:

`sudo apt-get install php-zip php-curl php-mbstring php-mysql php-gd php-dom`

You can make sure everything checks out by running `php -m` and look for all of these extensions. You can search for extensions by running something like `apt-cache search php- | grep mbstring` 

Next, there are other dependencies required. We don't need all of them, but I installed them all anyway because we had some trouble here, with the original installation.

One-liner to grab all the dependencies:
`sudo apt-get install graphicsmagick imagemagick ffmpeg dcraw pdfminer mediainfo exiftool xpdf libreoffice wkhtmltopdf`

To note the discrepenecy above and in the official docs: Ghostscript was already installed and qt-faststart is included in the FFmpeg installation.

I tested all these were installed by calling them:

`gm, convert, ffmpeg, dcraw, pdf2txt, mediainfo, exiftool, xpdf, libreoffice, wkhtmltopdf`


Now everything is there, but things aren't showing up if you go to your Droplet's URL.

I had to get Providence living in the right folder for serving over the web, and also modify some configuration files to do this. I followed yet another Digital Ocean docs page on [installing the apache web server](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-18-04-quickstart). I made a specific configuration file within `/etc/apache2/sites-available` so hitting the website would route to the correct place. 

The config file looks something like this:

```
<VirtualHost *:80>
    ServerAdmin admin@example.com
    ServerName my-cool-name
    ServerAlias my-cool-name
    DocumentRoot /var/www/my-cool-name
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

You'll probably have to `service apache2 reload` to see these changes.

When I cloned the Providence repository as instructed in the installation guide, I put it in `/var/www`, and kept it wrapped up in the `providence` folder. The instructions indicate that specific folders have their permissions opened up, so I did that by running `chmod -R` and opening up the settings on those temporary folders (and only those!).

The instructions indicate that you will need to edit a php.ini file. If using the same system as I am (Ubuntu 16.04), it's here:

`/etc/php/7.0/apache2/php.ini` 

I also made a new MySQL database with open read/write permissions (log in as root, CREATE DATABASE, and create a user that has full permissions on that database), and that is the information I stored in the setup.php file mentioned in the original instructions.

The rest of the installation can be done by going to /install wherever your site is installed. It will also warn you if some parts are missing, or if any of the above steps were missed. It won't warn you about the dependencies, however.

Now, the next steps for us are to test and make sure this installation is up to par, and then the next step for me is to do a migration of all the existing data onto these servers.

This would be a fun and small project to wrap up as a Docker image or something, but I am not going to do that, at least not without being compensated for my time. If you are installing Collective Access on a cloud-based server, I hope this helps save you some time!