# AI Security Scanner for Python

**Author:** Thomas Miller  
**Email:** tmiller1996.work@gmail.com

---

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/ai-security-audit_sec4e5f6)

---

## Introducing Today's Project!

In this project, I'm going to build a CLI AI Security Scanner for Python in order to detect code vulnerabilities. Examples could be hard coded secrets or weak cryptographic protocols being utilized.

### Key tools and concepts

The tools I used for this project were python and gemini. Key concepts I learnt include crafting structure prompts, securing keys, and python environment management with venv.

### Challenges

This project took me approximately 1 hour to complete. The most challenging part was expanding it to support dynamic inputs and I want to work on this in the future to accept multiple files at once.

### Why I did this project

I did this project today because I want to improve in regard to Security. This project met my goals by combining the hot topic of AI with Security. Next, I plan to develop my Cloud/Security skills further through additional projects.

---

## Connecting to Gemini API

To begin with, I'll be creating a dedicated space for my CLI AI Python Scanner, Generating a Google AI API Key, Setting up a .env file with that API Key, and testing (and verifying) the connection to Gemini

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/ai-security-audit_sec2c3d4)

I verified the connection by running py scanner.py Gemini responded with 'This test worked!' which confirmed that the API Key is correct and setup. It's important to note at this stage I originally used the google.generativeai library but once I ran the code I was getting warning about it no longer receiving support. Therefore, I changed over to the google.genai library which required a few changes as you have to specify the model you want to use in the request itself instead of beforehand.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/ai-security-audit_sec4e5f6)

My scanner.py file works by sending a prompt to gemini that contains a code extract. When I ran it, Gemini identified multiple isses with the code such as hardcoded secrets, a weak password, and a lack of secure authentication practices (hasing etc...). Additionally, Gemini provided recommendations for remediation of the aforementioned issues by outlining best practices for each issue. This shows that the Gemini API can detect vulnerabilities in code.

---

## Building the Vulnerability Scanner

Next, I'm building upon this vulnerability scanner to add additional vulnerable code examples to test against enabling the detection of SQL injection, hardcoded secrets, and weak cryptography. For thism I need to create a detailed security prompt for Gemini and create vulnerable code examples to test it against..

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/ai-security-audit_sec7h8i9)

The vulnerabilities Gemini detected were SQL Injection, Hardcoded Secrets, and Poor Crypography (md5). The security prompt I crafted was more advanced than the initial one as it set the scene for gemini prompting it to think like a security expert and outline very structured and concise responses regarding the code. This structured output helps provide an approach to identify what type of vulnerability it is, why it's vulnerable, what the impact is, and approaches to fix the code. Now, the walkthrough I'm doing has shown examples of pasting code into the scanner.py file in order to check if it's vulnerable. I don't think that is necessarily a scalable approach to security so I've implemented a way to scan external files in order to make the code dynamic. In the future I could add the ability to select a specific file (or group of files) from an interface.

---

## Adding Severity Ratings

In this step, I'm adding severity ratings which will highlight the urgency of each vulnerability. From a risk management perspective, this can support the categorisation and priotization of risk meaning we can deal with more urgent risks first.

To achieve this, I will be installing the python colorama library which enables me to provide a colored terminal output. I'll then test this to see if it works as expected. Additionally, I'll have to readjust the prompt in order for it to provide a severity rating: [CRITICAL/HIGH/MEDIUM/LOW].

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/ai-security-audit_sec0k1l2)

I updated the security prompt to include the aforementioned severity ratings and also used the colorama library in over to change the colour of command line text. Instead of just printing the output from Gemini straight into the terminal, the text gets passed through a function which checks for keywords to highlight.

---

## Scanning Real Python Files

Now that a baseline version of the program exists, I want to extend upon what I mentioned earlier develop the tool so that it can scan other python files. I think the approach i will take for this is accepting command-line arguments for file paths.

![Image](http://learn.nextwork.org/relieved_lavender_noble_bear/uploads/ai-security-audit_sec3n4o5)

I scanned vulnerable.py by running "py scanner.py vulnerable.py". There were a range of vulnerabilities in the python file including SQL injection, Weak Hasing Algorithms, Command Injections, and Hardcoded Credentials. To achieve this output, I created a scan_file function which takes in a command line argument and scans the file if it exists.

To improve upon this in the future I want to:
Scan entire directories - Loop through all specified file types in a folder
Generate reports - Save results to a JSON or HTML file

This tool could also be used for CI/CD integration enabling by making the scanner run on every commit.