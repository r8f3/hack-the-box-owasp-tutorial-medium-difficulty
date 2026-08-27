<iframe width="1308" height="736" src="https://www.youtube.com/embed/uZc52qu_oJw" title="owasp juice shop tutorial" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>




# prerequisite 
Having installed and configured Foxy Proxy, this is covered in the video above but will not be in the text guide. 

# Part One: Reconnaissance.
In part one of the challenge, we need to do some reconnaissance. the website. We will start by looking around the website and checking out the reviews.
Trying to see if we can discover anything of value for us. Once we have completed this first step, we will try searching something to see how the URL handles searches. 


# Part two: The admin account. 

## Step one: Burp Suite 
Once Burp Suite is open, navigate to the proxy tab. Once this is complete, return to the juice shop website. Click Account Login. 
Once you have arrived at the login page. make sure the interceptor and Foxy Proxy are turned on. Proceed to log in using the admin email(password does not matter; put anything) you should have found during step one.
If Foxy Proxy has been configured properly. you will see 3 packets.

## step 2 The attack. 
Now, of these 3 packets, we are looking for the one labeled "post" under the method category. Once you have navigated to this packet. Look through the packet for the "email and password field." Here we need to change the email to ** "' or 1=1--" **. Now, at the top of the proxy tab, click the down arrow and select forward all. Now click the big orange button, and congratulations, you have logged into the admin account through SQL. 
Why this works is because the input '1=1--' closes an open text field; 1=1 creates a logical condition that is always true, and -- comments out the rest of the original query so the database ignores the password check.
<img width="239" height="60" alt="image" src="https://github.com/r8f3/hack-the-box-owasp-tutorial-medium-difficulty/blob/main/sql%20injection.png" />

# Part 3 The Bender account

## Step one: the Bender account.
Works mostly the same as the last step, only this time we are using the bender account, which you should have discovered in your reconnaissance.
Recreate the login steps from the previous part of the challenge, although when we get to the stage of entering the SQL injection, we enter ** "bender@juice-sh.op'--" ** 
This works mostly the same as the previous task; what's changed is we don't need to force the database to think something is true, as we know the email is valid.

# Part 4 Brute forcing the admin account 

## Step one: navigate back to the login page.
Once you have tried to log in to the admin account and stalled the packet again, once we have found the login packet, we need to send it to the intruder.
Then we will add the special character symbols around the password section. On the right side, you can click Load Payload. If you navigate through / > usr > share > wordlists, you can load a wordlist from Kali's pre-installed wordlists. For my example, I just added words to the list and included the correct password. Once the brute force is completed, you can see all the attempts; you are looking for one that responded with code 200. This one will be a password that worked. 
<img width="239" height="60" alt="image" src="https://github.com/r8f3/hack-the-box-owasp-tutorial-medium-difficulty/blob/main/brute%20force.png" />

# Part 4 recovering Jim's account.
This is really an OSINT challenge. While doing reconnaissance, you should have come across Jim's account; reviewing his email is jim@juice-sh.op. 
If we navigate to Recover Account and enter his email, we can see what his security question is: "Your eldest sibling's middle name." We can figure this out by realizing he references Star Trek in his review; if we Google 
Jim Star Trek, we are able to see his family tree and find out his oldest sibling's middle name is Samuel, and just like that, we are able to circumvent the security question. 



































