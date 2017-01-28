#Cross Site Scripting (XSS)
XSS is the most common web application security flaw. XSS flaws occur when an application includes user supplied data in a page sent to the browser without properly validating or escaping that content. The three known types of XSS vulnerabilities that we will cover are:
* Reflected XSS
* Stored XSS
* DOM Based XSS

#Javascript
The magic behind XSS attacks if the Javascript language. Javascrip if the browser's language, and as such, whenever you have a webpage, you try to use javascripts to make it do what you want it do it. 
To demonstrate this, you can simply open up your favorite browser (I prefer chrome) and access the console in the developer tools. *In chrome, just right click anywhere, and select inspect. Now click the console tab.*
In the console you can execute any piece of javascript you want to for testing purposes. However, it won't actually impact anyone else. Try executing the following:
```
console.log('Does this even work?');
alert('I am a bAd@$$ H@cK3r');
```


##Reflected XSS
