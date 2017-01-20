# Web-Security-I
In this blog, I will be keeping track of my thoughts and notes for a web security I course. I hope this notes and excersizes will be useful to other professors and students in the future. 

##Intro
In this course, I will be focusing on the Open Web Application Security Project (OWASP) top 10 vulnerabilities list which can be found [here](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet). More specifically, these exercises will demonstrate how to exploit the vulnerabilities on a given web application. This approach is chosen because it is crucial to practically understand how a vulnerability works in order to even care about defending against it. 

As a lazy programmer, I will admit that my own apps aren't always completely secure. But who cares about my stupid apps anyways? Probably no one, but there are thousands of automated vulnerability scanners and script kiddies out there looking to pwn someone around the clock. And if your application matters to anyone (even just you), then you don't want to get caught with your pants down. 

Of course, it isn't exactly practical to create exercises for all of the items on the OWASP top 10 list, so I will focus only on a couple for now. Namely:
* SQL injections 
* Cross Site Scripting (XSS)
* Cross Site Request forgery (CSRF)
* Unvalidated Redirects or forwards 
* Session HijackingS
* Insecure Direct Object Reference

https://www.owasp.org/images/f/f8/OWASP_Top_10_-_2013.pdf

##BWapp
Throughout this tutorial, I will be using the [bwapp](http://www.itsecgames.com/) web application for testing purposes. This is a vulnerable application that was created for crappy-hackers like you and I to get some experience without getting arrested. 

Installing bwapp on your machine can be a pain (installing and configuring a local database and messing with settings are bleh). So being the lazy programmers we are, we are going to cheat. OWASP actually has a collection of vulnerable applications available on a virtual machine for us [including bwapp](https://www.owasp.org/index.php/OWASP_Broken_Web_Applications_Project), which gives a lot more bang for a lot less buck. Go ahead and download the VM. You are also going to need [virtualbox](https://www.virtualbox.org/wiki/Downloads). The setup process is a bit tricky but I walk you through it in this [short video](https://www.youtube.com/watch?v=Y9Q0u045KJg). *Ignore the fact that I say pentesterlab in the walkthrough. The tutorial applies for any such vm*.

##SQL Injection
Structure Query Language (SQL) is used to many developers to insert and retrieve information from a common relational database. Whenever you see a website that does more than just display static information (i.e. letting users make posts or create accounts) it is most likely using a database. Most Wordpress sites run on SQL databases. The standard SQL command looks like this:
```sql
select * users where name='Simeon'
```
This sql would statement simply pull my account information within a web application. In a web application, the developer might dynamically generate a sql statement based on the user input. 
```sql
select * users where name=[NAME]
```


