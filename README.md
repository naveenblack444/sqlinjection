# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2
# OUTPUT
![1](https://github.com/user-attachments/assets/f11935a1-9bb5-44a5-8eec-398ed29c3915)


Use the above ip address to access the apache webserver of Metasploitable2 from kali/parrot linux. In Kali Linux use the ip address in a web browser.
##  OUTPUT
![Alt text](img/2.png)

Select Multidae from the menu listed as shown above. The page is displayed as below:
##  OUTPUT
![Alt text](img/3.png)


Click on the menu Login/Register and register for an account
##  OUTPUT
![Alt text](img/4.png)


Click on the link “Please register here”
##  OUTPUT
![Alt text](img/5.png)
![Alt text](img/6.png)

Click on “Create Account” to display the following page:
##  OUTPUT
![Alt text](img/7.png)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:


($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
##  OUTPUT
![Alt text](img/7.png)


Click “Login”. The logged in page will show as below:
##  OUTPUT
![Alt text](img/8.png)


If error faced in registration follow the following steps in metasploitable 2:


This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:
cd /
sudo nano /var/www/mutillidae/config.inc
Type msfadmin when prompted for the root password. 
Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure  below:
##  OUTPUT
<img width="817" height="454" alt="{FD6DBF6E-F9DA-43E0-B240-40912CA88E61}" src="https://github.com/user-attachments/assets/cdf98714-105f-45c7-8ba9-a10bdbe0dc46" />



Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure
##  OUTPUT

<img width="816" height="445" alt="{7E11C84C-80D7-4E5A-BC1D-639530FAC203}" src="https://github.com/user-attachments/assets/91cd3f39-f9d1-4e1c-beb9-3456cb1f2ea0" />



Save and exit the config.inc
Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file
Restart the Apache server
To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM.
sudo /etc/init.d/apache2 reload
##  OUTPUT

<img width="815" height="97" alt="{B1B6E301-5B26-40F7-BFA7-BECE0F5883B1}" src="https://github.com/user-attachments/assets/7ba49990-1981-406c-812b-13a378f3c206" />



# Reset Mutillidae database
Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.
##  OUTPUT

<img width="1045" height="219" alt="image" src="https://github.com/user-attachments/assets/b1b00eae-024c-446a-bc1e-55b4b4a65958" />




# Test the new configuration
Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

 The Mutillidae database error no longer appears 
# OUTPUT
<img width="1038" height="386" alt="{7CC834CE-6793-4B07-8D53-901D843DF1D2}" src="https://github.com/user-attachments/assets/4c09d6f0-17e8-4533-a855-0998d0a1c95e" />



Now after logging out you will see the login page. In the login page give ganesh’ # (myusername). You can see the page now enters into the administrator page as before when giving the password.
# OUTPUT
![Alt text](img/7.1.png)

Click the login button and you will see it enter into the administrator page.
# OUTPUT
![Alt text](img/8.png)


## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:
##  OUTPUT
![Alt text](img/9.png)
![Alt text](img/10.png)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
##  OUTPUT

<img width="821" height="613" alt="{CB2C380F-1857-4A50-BE0A-9B874D6FEA46}" src="https://github.com/user-attachments/assets/d918e7ef-adb1-43aa-b196-e0aceb246f73" />


Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
##  OUTPUT

<img width="818" height="582" alt="{C0721B3F-1E9B-43BB-86C7-FEB9D2132BC0}" src="https://github.com/user-attachments/assets/442c9c01-48a7-4627-a0ce-c086ba0e9a6f" />



After adding the order by 6 into the existing url , the following error statement will be obtained:
##  OUTPUT

<img width="819" height="595" alt="{BDFA56C4-5A37-4A04-A9D9-42C52E9F45DB}" src="https://github.com/user-attachments/assets/22e3b908-40ea-4d35-ac7b-0bf0efc2b652" />



When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
# OUTPUT

<img width="814" height="578" alt="{99B07BC3-30CC-4F70-846C-A7F8D9AD61C2}" src="https://github.com/user-attachments/assets/87ab5613-709f-4e0e-9172-f8397c727b6f" />



 As it is having 5 columns the query worked fine and it provides the correct result
##  OUTPUT
![Alt text](img/10.png)



Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).
##  OUTPUT

<img width="811" height="454" alt="{68D75BBE-8CC9-4BCE-9F17-FA185C55F014}" src="https://github.com/user-attachments/assets/c9f612fa-0a2d-431d-8886-f990ccfa7d25" />


As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
##  OUTPUT

![Alt text](img/10.png)

<img width="1630" height="299" alt="{513549B9-3BA2-49C3-81B2-47CD30585451}" src="https://github.com/user-attachments/assets/ebc38bb4-26c3-409d-a443-ea6a82ef8035" />




Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
##  OUTPUT
![Alt text](img/10.png)
<img width="1625" height="289" alt="{BA67EC4A-F0ED-4E89-91A6-C3A9C504C53F}" src="https://github.com/user-attachments/assets/b8da79a1-a4fa-487f-aa66-d639a5522ecc" />


The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
##  OUTPUT
<img width="815" height="327" alt="image" src="https://github.com/user-attachments/assets/4f12bc71-d756-48e0-b8df-cc6d48e5c8a4" />


![Alt text](img/10.png)
<img width="1361" height="300" alt="{046FEEA0-1991-413E-A04D-63F846A6E1BB}" src="https://github.com/user-attachments/assets/f34867cb-7c2d-4dda-af37-9222d8cb6b93" />



The url once executed will  retrieve table names from the “owasp 10” database.
##Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
##  OUTPUT
<img width="818" height="251" alt="{2B5217CF-F998-468A-8946-C88F91FBCD47}" src="https://github.com/user-attachments/assets/56d4e274-df11-4683-a432-f6c550f6f896" />

![Alt text](img/10.png)
<img width="929" height="254" alt="{0237D909-2F7C-4E81-AEA2-B9E2AEA2D62B}" src="https://github.com/user-attachments/assets/4f174f29-6d7b-44d7-843d-ddb7a270ddef" />

The column names of the accounts is displayed below for the following url:


Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).
##  OUTPUT
![Alt text](img/10.png)
<img width="1633" height="388" alt="{C87EBB43-E375-4097-9B57-56009D06BB59}" src="https://github.com/user-attachments/assets/a54f48fe-1612-4d69-91e3-d17f15627618" />



## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).


##  OUTPUT
![Alt text](img/10.png)
<img width="1629" height="301" alt="{69C7F7B2-5554-4DED-A99D-5D0B8E8E6767}" src="https://github.com/user-attachments/assets/bb7ba56e-708e-465a-8e86-6dff17ace99d" />


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
