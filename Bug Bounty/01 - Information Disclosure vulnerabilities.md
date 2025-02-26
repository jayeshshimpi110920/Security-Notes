Following are the step approch to find out information disclosure vul.

1) **/robots.txt** - ```https://target.com/robots.txt```
 Google search have two main jobs:
* crawling the web to discover content
* indexing that content so that it can be served up to searchers who are looking for information

![image](https://github.com/user-attachments/assets/34049c04-69ff-45df-a842-69909163b973)

NOTE: try to navigate with path which is **_Disallow_** , if nevigate , boom see something intersting we might got. 

2) In above we discover ```/robots.txt``` path only, there might be possible more hidden path
   - TO find out for more directory, we use tool **FEROXBUSTER**- kind of fuzzing tools, to find more hidden path that might contant sensitive information.
   - `./feroxbuster --url https://target.com --depth 2 --wordlist words`
