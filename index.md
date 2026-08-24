
#prerequisite 
having installed and configured foxy proxy this is covered in the video above but will not be in the text guide 

# Part One reconnaissance .
In part one of the challenge we need to do reconnaissance on the website we will start by looking around the website try checking out the reviews.
Trying to see if we can discover anything of value for us. once we have completed this first step we will try searching something to see how the url handles searches. 


# Part two The admin account. 

## step one burp suite 
Once burp suite is open navigate to the proxy tab. once this is complete return to the juice shop website. click account log in. 
once you have arrived at the login page. make sure the interceptor and foxy proxy are turned on. proceed to login using the admin email(password does not matter put anything) you should have found during step one.
if foxy proxy has been configured properly. you will see 3 packets.

## step 2 The attack. 
Now of these 3 packets we are looking for the one labeled "post" under the method category once you have navigated to this packet. look through the packet for the "email and password field" here we need to change the email to ** "' or 1=1--" ** now at the top of the proxy tab click the down arrow and select forward all. now click the big orange button and congratulation you have logged into the admin account through sql. 
why this works is because The input '1=1-- the ' closes an open text field 1=1 creates a logical condition that is always true and -- comments out the rest of the original query so the database ignores the password check

# Part 3 The Bender account

## step one the bender account.
works mostly the same as the last step only this time we are using the bender account which you should have discovered in your reconnaissance.
recreate the login steps from the previous part of the challenge although when we get to the stage of entering the sql injection we enter ** "bender@juice-sh.op'--" ** 
this works mostly the same as the previous task what's changed is we dont need to force the database to think something is true as we know the email is valid.

# Part 4 Brute forcing the admin account 

## step one navigate back to the login page.
once you have tried to login to the admin account and stalled the packet again once we have found the login packet we need to send it to the intruder.
then we will add the special character symbols around the password section. on the right side you can click load payload. if you navigate through / > usr > share > wordlists 
and you can load a wordlist from kali's pre-installed wordlists. for my example i just added words to the list and included the correct passport. once the brute force is completed you can see all the attempts you are looking for one that responded with code 200 this one will be a password that worked. 

# Part 4 recovering jim's account.
This is really a osint challenge while doing reconnaissance you should have come across jim's account review his email is jim@juice-sh.op. 
if we navigate to recover account and enter his email we can see what his security question is "Your eldest siblings middle name" we can figure out this by realizing he references star trek in his review if we google 
jim star trek we are able to see his family tree and find out his oldest siblings middle name is Samuel and just like that we are able to circumvent the security question. 















































