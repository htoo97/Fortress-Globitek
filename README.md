# Project 10 - Fortress Globitek

Time spent: **2** hours spent in total

> Objective: Create an intentionally vulnerable version of the Globitek application with a secret that can be stolen.

### Requirements

- [x] All source code and assets necessary for running app
- [x] `/globitek.sql` containing all required SQL, including the `secrets` table
- [x] GIF Walkthrough of compromise
- [x] Brief writeup about the vulnerabilities introduced below

<img src='http://i.imgur.com/lNX76kJ.gif' title='walkthrough' alt='fortress-globitek'>

### Vulnerabilities

Describe the vuln(s) here.

The salesperson url is vulnerable to sql injection. We can use it to exploit the sql union operator to get the data from the secret column in secrets table. To do that, we find the number of columns of the salesperson table first by using 'order by' incrementing the number until database query error is returned, indicating the last order by number was the last column number and hence the number of columns in the salesperson table. Using that information, a union statement can be constructed using a nonexistent id (0), followed by five columns of secret from the secrets table, revealing the information we need. Essentially, the whole sql statement is as follows:
```
SELECT * FROM salespeople where id='0' UNION SELECT secret, secret, secret, secret, secret FROM secrets; -- randomasdf
```
