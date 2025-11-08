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
#OUTPUT
<img width="1064" height="518" alt="image" src="https://github.com/user-attachments/assets/f1b18d1b-5f60-4cb9-a883-7fe247451be2" />

Use the above ip address to access the apache webserver of Metasploitable2 from kali/parrot linux. In Kali Linux use the ip address in a web browser.
##  OUTPUT
<img width="931" height="606" alt="image" src="https://github.com/user-attachments/assets/a2e159be-43d7-4eb7-9241-b259942e153f" />


Select Multidae from the menu listed as shown above. The page is displayed as below:
##  OUTPUT

<img width="1032" height="475" alt="Screenshot 2025-11-08 104354" src="https://github.com/user-attachments/assets/fe29ef2d-16d3-4f86-8002-b6b998b731ea" />


Click on the menu Login/Register and register for an account
##  OUTPUT

<img width="1031" height="465" alt="image" src="https://github.com/user-attachments/assets/3cf6da57-8ddc-461c-a2e5-7384fa7bfa8b" />



Click on the link “Please register here”
##  OUTPUT


<img width="1033" height="460" alt="image" src="https://github.com/user-attachments/assets/23a9979f-b356-44f1-90b9-6e80bc3df847" />


Click on “Create Account” to display the following page:
##  OUTPUT


<img width="1035" height="399" alt="image" src="https://github.com/user-attachments/assets/8795d64a-b957-48e0-b992-423e5fca138d" />

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:


($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
##  OUTPUT

<img width="1036" height="452" alt="image" src="https://github.com/user-attachments/assets/1b6c0d63-9cc8-4d06-a38a-d0e996406bf7" />



Click “Login”. The logged in page will show as below:
##  OUTPUT



<img width="1022" height="558" alt="image" src="https://github.com/user-attachments/assets/6467fab4-6cde-4acc-aba9-323951b3ea16" />

If error faced in registration follow the following steps in metasploitable 2:


This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc
Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]:
cd /
sudo nano /var/www/mutillidae/config.inc
Type msfadmin when prompted for the root password. 
Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure  below:
##  OUTPUT

<img width="1040" height="449" alt="image" src="https://github.com/user-attachments/assets/96afae81-3348-4963-8936-1088e66713f5" /

## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:
##  OUTPUT


<img width="1040" height="358" alt="image" src="https://github.com/user-attachments/assets/f164c767-b0ce-49f7-92f9-879f56b8a336" />


From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
##  OUTPUT

<img width="1022" height="426" alt="image" src="https://github.com/user-attachments/assets/bfc409a8-58ce-4899-983b-2da0524c842b" />




Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.
After adding the order by 6 into the existing url , the following error statement will be obtained:
##  OUTPUT
<img width="1021" height="435" alt="image" src="https://github.com/user-attachments/assets/294d16f3-1867-460d-bb8e-5b4364114985" />

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
#OUTPUT
<img width="1032" height="266" alt="image" src="https://github.com/user-attachments/assets/a9237780-3e3a-47f2-9b28-d56f40f49090" />

 As it is having 5 columns the query worked fine and it provides the correct result
##  OUTPUT
<img width="1017" height="511" alt="image" src="https://github.com/user-attachments/assets/e9401068-71b6-4010-bf7a-c3e69ae2de6c" />
Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).
##  OUTPUT
<img width="1051" height="135" alt="image" src="https://github.com/user-attachments/assets/03e2837f-4196-4cb5-b67f-df1d7e5dc77a" />
As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
##  OUTPUT
<img width="1017" height="550" alt="image" src="https://github.com/user-attachments/assets/ba7739e4-8e31-491b-8733-af6cb9ff52f3" />
Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
##  OUTPUT


<img width="1017" height="550" alt="image" src="https://github.com/user-attachments/assets/26076bf7-f6e3-473a-9174-4d6f8fbbdfaa" />


The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
##  OUTPUT

<img width="1013" height="443" alt="image" src="https://github.com/user-attachments/assets/0da670ec-413b-4699-a2a1-0335ac5ed6d9" />

The column names of the accounts is displayed below for the following url:


Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
