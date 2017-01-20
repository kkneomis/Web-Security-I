# Web-Security-I
In this blog, I will be keeping track of my thoughts and notes for a web security I course. I hope this notes and excersizes will be useful to other professors and students in the future. 

###Intro
In this course, I will be focusing on the Open Web Application Security Project (OWASP) top 10 vulnerabilities list which can be found [here](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet). More specifically, these exercises will demonstrate how to exploit these vulnerabilities on a given web application. This approach is chosen because it is crucial to practically understand how a vulnerability works in order to even care about defending against it. 

As a lazy programmer, I will admit that my own apps aren't always completely secure. But who cares about my stupid apps anyways? Probably no one, but there are thousands of automated vulnerability scanners and script kiddies out there looking to pwn someone around the clock. And if your application matters to anyone (even just you), then you don't want to get caught with your pants down. 

Of course, it isn't exactly practical to create exercise for all of the items on the OWASP top 10 list, so I will focus only on a couple for now. Namely:
* SQL injections 
* Cross Site Scripting (XSS)
* Cross Site Request forgery (CSRF)
* Unvalidated Redirects of forwards 
* Session Hijacking
* Insecure Direct Object Reference


https://www.owasp.org/images/f/f8/OWASP_Top_10_-_2013.pdf
