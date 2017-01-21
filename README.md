# Web-Security-I
In this blog, I will be keeping track of my thoughts and notes for a web security I course. I hope these notes and exercises will be useful to other professors and students in the future. 

##Intro
In this course, I will be focusing on the [Open Web Application Security Project (OWASP) top 10 vulnerabilities list](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet). More specifically, these exercises will demonstrate how to exploit the vulnerabilities on a given web application. This approach is chosen because it is crucial to practically understand how a vulnerability works in order to even care about defending against it. 

As a lazy programmer, I will admit that my own apps aren't always completely secure. But who cares about my stupid apps anyways? Probably no one, but there are thousands of automated vulnerability scanners and script kiddies out there looking to pwn someone around the clock. And if your application matters to anyone (even just you), then you don't want to get caught with your pants down. Additionally, I vulnerable wep app puts everyone in danger including your users, your organization, yourself, and your reputation.

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
Structured Query Language (SQL) is used to many developers to insert and retrieve information from a common relational database. Whenever you see a website that does more than just display static information (i.e. letting users make posts or create accounts) it is most likely using a database. Most Wordpress sites run on SQL databases. The standard SQL command looks like this:
```sql
select * users where name='Simeon'
```
This sql would statement simply pull my account information within a web application. In a web application, the developer might dynamically generate a sql statement based on the user input. 

Suppose the developer wanted to select users based on your input, the sql statement might look like this:
```sql
select * users where name='[NAME]'
```
The problem with this is that you (you sneaky person you ;] ) might try to enter a value to break that sql statement or use it to extract more information from the database than you are entitled to (usernames, passwords, ssn numbers, etc...).

Let's start with the bwapp SQL Injection (Search/GET) exercise.

You should begin by playing around with the search box and entering various values to see what happens. If you simply press enter, all the movies are returned. However, if you enter a single quote ', you get the following error
```
Error: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '%'' at line 1
```
This is because you have broken the dynamic sql statement was supposed to be generated from your input (congratulations on being a bAd@$$-H@CK3R!). We can assume the sequel statement looked something like this:
```
select * from movie where title=' + [YOUR INPUT] + '
```
I can tell by looking at the url ;). By inputing a single quote, or anything followed by a single quote, you break the sql statement because it now has too many quotes. Suppose you entered "iron man'", then the resulting sql statement would be:
```
select * from movie where title='iron man''
```
That's one quote too many! And sql being picky with syntax has no idea how to interpret that. If you ever get this result on any website, you are clear to wreak havoc (at your own risk, of course).
 
For this next section, we'll switch from using the input field to messing with the url of the page. This will work because the input is being submitted though a GET request. Go ahead and give it a try! Instead of search using the input box, just replace everything after the "?title=" in the url with your search term. You should get the same results as using the search box. 

First, we'll try to guess how many tables are in database!

We can achieve this using sql's ORDER BY command. You can use it like so:
```
http://192.168.1.250/bWAPP/sqli_1.php?title=1' ORDER BY 99-- -
```
First we should recognize that the sql command outputed from like probably looks like:
```
select * from movie where title='1' ORDER BY 99-- -
```
The "-- -" is the SQL syntax for commenting. We want to negate anything that comes after our input so we can be sure about the command's behavior. 

You should get an error from the command above. Since we will always get an error if we order by more than the number of tables that exist, we can keep trying it with a small number until we no longer get an error. At that point we will know how many tables exist in the database. 

If you order order by any number less than 7, you should no longer have an error. Instead, it should say "No movies were found!". Great! We'll use this information going forward.