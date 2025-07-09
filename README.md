# My Journey with Agentic AI Part 1: From Scratch: LLM Workflows Minus the Magic Tools (Lab 1)

This Jupyter Notebook (`1_lab1.ipynb`) serves as the introductory lab for a course on Agentic AI, guiding users through setting up their environment, interacting with the Azure OpenAI API, and performing basic AI-driven tasks without relying on high-level frameworks or "magic tools." It includes setup instructions, Python code for API interactions, and an exercise to explore commercial applications of Agentic AI. Below is a detailed breakdown of each cell, organized by purpose and content, presented in a clear, meaningful format.

## Section 1: Course Introduction and Setup

### Welcome Message
- **Purpose**: Introduces users to the Agentic AI course with enthusiasm.
- **Content**: 
  - Title: `# Welcome to the start of your adventure in Agentic AI`
  - Sets the tone for an exciting learning journey focused on building AI workflows from scratch.

### Setup Confirmation
- **Purpose**: Ensures users have completed prerequisite setup steps.
- **Content**:
  - Displays a table with a `stop.png` image and orange text (`#ff7800`).
  - Prompts users to confirm completion of:
    - Setup steps in the `../setup/` folder.
    - Review of guides in `../guides/01_intro.ipynb`.
  - Confirms readiness with: “Well in that case, you're ready!!”

### Live Resource Notification
- **Purpose**: Informs users that the notebook is a dynamic, evolving resource.
- **Content**:
  - Table with a `tools.png` image and blue text (`#00bfff`).
  - Explains that the notebook is updated based on user feedback and may differ from accompanying videos.
  - Notes regular email updates via Udemy’s “Announcements” section and advises enabling notifications in Udemy’s Notification Settings.
  - Emphasizes respectful, value-driven email communication.

### Support and Jupyter Setup Instructions
- **Purpose**: Provides instructor contact information and detailed setup instructions for Jupyter notebooks in Cursor (a VS Code-based editor).
- **Content**:
  - Encourages contacting the instructor via LinkedIn: `https://www.linkedin.com/in/eddonner/`.
  - Guides users to install Python and Jupyter extensions in Cursor:
    - Open extensions (`View >> Extensions`).
    - Install `ms-python` (Python) and `Microsoft` (Jupyter) extensions if not already installed.
    - Return to File Explorer (`View >> Explorer`).
  - Instructs on selecting the Python kernel:
    - Click “Select Kernel” (top right) and choose `.venv (Python 3.12.9)` or similar.
    - If not visible, select “Python Environments” first.
    - Run cells by clicking and pressing `Shift+Enter`.
  - Troubleshooting for missing kernel:
    - Adjust settings in `VS Code Settings` (not `Cursor Settings`).
    - Search for “venv” and set the virtual environment path (e.g., `C:\Users\username\projects\agents` on Windows or `/Users/username/projects/agents` on Mac/Linux).
  - Addresses Anaconda interference:
    - Deactivate Anaconda environment: `conda deactivate`.
    - Disable auto-activation: `conda config --set auto_activate_base false`.
    - Verify Python 3.12 version: `uv python list` in the `agents` directory.

## Section 2: Environment Setup and API Key Loading

### Import `dotenv`
- **Purpose**: Imports the `dotenv` library to manage environment variables.
- **Code**:
  ```python
  # First let's do an import
  from dotenv import load_dotenv
  ```
- **Explanation**: Imports `load_dotenv` to load API keys from a `.env` file, a foundational step for secure API access.

### Load Environment Variables
- **Purpose**: Loads API keys from the `.env` file into the environment.
- **Code**:
  ```python
  # Next it's time to load the API keys into environment variables
  load_dotenv(override=True) # this code will look for a .env file in the current directory where what is in the .env file takes priority over the environment variables
  ```
- **Output**: `True`
- **Explanation**: Loads variables from `.env`, prioritizing them over existing environment variables. Returns `True` if successful.

### Troubleshoot `.env` Issues
- **Purpose**: Provides guidance if `load_dotenv` returns `False`.
- **Content**:
  - Identifies common issues: `.env` file not saved or incorrectly named/located.
  - Instructs users to:
    - Save the `.env` file.
    - Ensure it’s named exactly `.env` and located in the project root (`agents` directory).
  - Notes that Cursor marks `.env` with a stop symbol to protect sensitive data from being shared with external AI.

### Final Reminders
- **Purpose**: Offers additional resources for foundational knowledge.
- **Content**:
  - Table with `stop.png` image and orange text (`#ff7800`).
  - Recommends reviewing:
    - Topics 3 and 5 in `../guides/04_technical_foundations.ipynb` for Environment Variables and Web Endpoints/APIs.
    - First section of `../guides/09_ai_apis_and_ollama.ipynb` for using alternative AI APIs (e.g., Gemini, DeepSeek, or Ollama).
    - Last section of `../guides/06_python_foundations.ipynb` for fixing Python Name Errors.

## Section 3: Azure OpenAI API Interaction

### Check Azure OpenAI Key
- **Purpose**: Verifies the presence of the Azure OpenAI API key.
- **Code**:
  ```python
  # Check the key - if you're not using OpenAI, check whichever key you're using! Ollama doesn't need a key.
  '''
  import os
  openai_api_key = os.getenv('OPENAI_API_KEY')
  if openai_api_key:
      print(f"OpenAI API Key exists and begins {openai_api_key[:8]}")
  else:
      print("OpenAI API Key not set - please head to the troubleshooting guide in the setup folder")
  '''
  import os
  from dotenv import load_dotenv
  load_dotenv()
  azure_openai_key = os.getenv("AZURE_OPENAI_KEY")
  if azure_openai_key:
      print(f"Azure OpenAI Key exists and begins with: {azure_openai_key[:8]}")
  else:
      print("Azure OpenAI Key not set — please check your .env file")
  # above one is for openai api key , i am using Azure student api key under the 100 dolar cridt option so i am chainging it to below one :
  ```
- **Output**: `Azure OpenAI Key exists and begins with: DYtXm4HS`
- **Explanation**: Checks for the `AZURE_OPENAI_KEY` environment variable, printing the first 8 characters if present. Includes commented-out code for OpenAI API key checking.

### Import Azure OpenAI
- **Purpose**: Imports the Azure OpenAI client library.
- **Code**:
  ```python
  # And now - the all important import statement
  # If you get an import error - head over to troubleshooting in the Setup folder
  # If you get a Name Error - head over to Python Foundations guide (guide 6)
  # from openai import OpenAI   ( use this if you're using OpenAI) , i am using together_ai_api so i am chainging 
  from openai import AzureOpenAI # i am using azure openai so i am chainging it to below one :
  ```
- **Explanation**: Imports `AzureOpenAI` from the `openai` package, with a note to use `OpenAI` for standard OpenAI API users.

### Create Azure OpenAI Client
- **Purpose**: Initializes an Azure OpenAI client instance.
- **Code**:
  ```python
  # And now we'll create an instance of the OpenAI class
  # If you're not sure what it means to create an instance of a class - head over to the guides folder (guide 6)!
  # If you get a NameError - head over to the guides folder (guide 6)to learn about NameErrors - always instantly fixable
  # If you're not using OpenAI, you just need to slightly modify this - precise instructions are in the AI APIs guide (guide 9)
  # openai = OpenAI()  ( use this if u have open api key , i don't so using togther_ai_api )
  # Create a client instance to call Azure OpenAI APIs
  client = AzureOpenAI(
      api_key=os.getenv("AZURE_OPENAI_KEY"),
      api_version="2025-01-01-preview",
      azure_endpoint="https://vishv-mcf4rawt-eastus2.cognitiveservices.azure.com"
  )
  # i am using azure openai 
  ```
- **Explanation**: Creates an `AzureOpenAI` client with the API key, version, and endpoint specific to the user’s Azure deployment.

### Simple API Call (2+2)
- **Purpose**: Demonstrates a basic API call to compute 2+2.
- **Code**:
  ```python
  # Create a list of messages in the familiar OpenAI format
  messages = [{"role": "user", "content": "What is 2+2?"}]
  ```
  ```python
  # And now call it! Any problems, head to the troubleshooting guide
  # This uses GPT 4.1 nano, the incredibly cheap model
  # The APIs guide (guide 9) has exact instructions for using even cheaper or free alternatives to OpenAI
  '''
  response = openai.chat.completions.create(
      model="gpt-4.1-nano",
      messages=messages
  )
  print(response.choices[0].message.content)
  '''
  #use above one if u have open api key , i don't so using Azure openai api key) , see below :
  # Call the model and print the response
  response = client.chat.completions.create(
      model="gpt-4o-mini",  # This must match your Azure deployment name
      messages=messages
  )
  print(response.choices[0].message.content)
  ```
- **Output**: `2 + 2 equals 4.`
- **Explanation**: Sends a user message (“What is 2+2?”) to the `gpt-4o-mini` model and prints the response. Includes commented-out code for OpenAI’s `gpt-4.1-nano`.

### Generate a Challenging Question
- **Purpose**: Asks the model to propose a hard IQ question.
- **Code**:
  ```python
  # And now - let's ask for a question:
  question = "Please propose a hard, challenging question to assess someone's IQ. Respond only with the question."
  messages = [{"role": "user", "content": question}]
  ```
  ```python
  # ask it - this uses GPT 4.1 mini, still cheap but more powerful than nano
  response = client.chat.completions.create(
      model="gpt-4o-mini",
      messages=messages
  )
  question = response.choices[0].message.content
  print(question)
  ```
- **Output**: `If a cat has four legs and a dog has four legs, how many legs do three cats and two dogs have in total?`
- **Explanation**: Requests a challenging IQ question and stores the response.

### Answer the Generated Question
- **Purpose**: Asks the model to answer the generated question.
- **Code**:
  ```python
  # form a new messages list
  messages = [{"role": "user", "content": question}]
  ```
  ```python
  # Ask it again
  response = client.chat.completions.create(
      model="gpt-4o-mini",
      messages=messages
  )
  answer = response.choices[0].message.content #this is the simplest way to call opeanai from clpud for chat completion
  print(answer)
  ```
- **Output**:
  ```markdown
  To find the total number of legs for three cats and two dogs, we can begin by calculating the number of legs each animal has.
  - A cat has 4 legs. Therefore, three cats have:  
    \(3 \text{ cats} \times 4 \text{ legs/cat} = 12 \text{ legs}\).
  - A dog also has 4 legs. Therefore, two dogs have:  
    \(2 \text{ dogs} \times 4 \text{ legs/dog} = 8 \text{ legs}\).
  Now, we can add the legs of the cats and the dogs together:  
  \(12 \text{ legs (from cats)} + 8 \text{ legs (from dogs)} = 20 \text{ legs}\).
  So, in total, three cats and two dogs have 20 legs.
  ```
- **Explanation**: Sends the generated question to the model and prints the detailed response.

### Display Answer in Markdown
- **Purpose**: Renders the answer in a formatted Markdown display.
- **Code**:
  ```python
  from IPython.display import Markdown, display
  display(Markdown(answer))
  ```
- **Output**: Formatted Markdown display of the answer (same as above).
- **Explanation**: Uses IPython’s `Markdown` and `display` to render the answer with proper formatting.

### Congratulations Message
- **Purpose**: Congratulates users on completing the first lab.
- **Content**:
  - Title: `# Congratulations!`
  - Notes that this is a small step toward Agentic AI and promises more interesting content in future labs.

## Section 4: Commercial Application Exercise

### Exercise Description
- **Purpose**: Introduces an exercise to explore commercial applications of Agentic AI.
- **Content**:
  - Table with an `exercise.png` image and orange text (`#ff7800`).
  - Tasks:
    1. Ask the LLM to pick a business area for Agentic AI opportunities.
    2. Ask the LLM to identify a pain point in that industry suitable for an Agentic solution.
    3. Ask the LLM to propose an Agentic AI solution.
  - Encourages users to try despite uncertainty, as the topic will be covered in upcoming labs.

### Business Area Selection
- **Purpose**: Asks the model to select a business area in the IT sector for Agentic AI opportunities.
- **Code**:
  ```python
  # First create the messages:
  messages = [{"role": "user", "content": "pick a business area that might be worth exploring for an Agentic AI opportunit within the next 10 years in the IT sector"}]
  # Then make the first call:
  response = client.chat.completions.create(
      model="gpt-4o-mini",
      messages=messages
  )
  # Then read the business idea:
  business_idea = response.choices[0].message.content
  print(business_idea)
  ```
- **Output**:
  ```markdown
  One promising business area worth exploring for Agentic AI opportunities in the IT sector within the next decade is **Cybersecurity Automation and Response**.
  ### Rationale:
  1. **Increased Cyber Threats**: The frequency and sophistication of cyberattacks are on the rise...
  2. **Complexity of IT Environments**: As organizations increasingly adopt multi-cloud environments...
  3. **Adaptive Learning**: Agentic AI systems can continuously learn from new threats...
  4. **Integration with Existing Tools**: There is an opportunity for Agentic AI to integrate with existing cybersecurity tools...
  5. **Incident Response**: Developing AI agents that can autonomously respond to certain types of incidents...
  6. **Privacy and Compliance**: Agentic AI can assist organizations in ensuring compliance...
  7. **Scalability**: As small to medium-sized enterprises (SMEs) become targets of cybercriminals...
  ### Potential Business Models:
  - **Managed Security Services**: Offering a subscription-based service...
  - **Security Software Development**: Creating software solutions...
  - **Consulting Services**: Assisting organizations in integrating Agentic AI...
  ### Conclusion:
  Given the increasing importance of cybersecurity in a digitally evolving world...
  ```
- **Explanation**: Identifies **Cybersecurity Automation and Response** as a promising area, with detailed rationale and business models.

### Empty Markdown Cell
- **Purpose**: Placeholder (no content).
- **Content**: Empty.

### Identify Pain Point
- **Purpose**: Asks the model to identify a pain point in the IT industry suitable for an Agentic solution.
- **Code**:
  ```python
  # Ask it again ( this time with the  present a pain-point in that industry - something challenging that might be ripe for an Agentic solution)
  question = "ppls concider the present a pain-point in that industry ( ie the it industry that we discussed earlier ) - something challenging that might be ripe for an Agentic solution"
  messages = [{"role": "user", "content": question}]
  response = client.chat.completions.create(
      model="gpt-4o-mini",
      messages=messages
  )
  answer = response.choices[0].message.content
  print(answer)
  ```
- **Output**:
  ```markdown
  In the IT industry, several pain points have become increasingly prominent...
  1. **Skill Gaps and Talent Shortages**: The IT industry is facing a significant skills gap...
  2. **Cybersecurity Threats**: As cyberattacks become more sophisticated...
  3. **Remote Work Challenges**: The shift to remote work has introduced challenges...
  4. **Project Management Inefficiencies**: Many IT projects suffer from delays...
  5. **Legacy System Integration**: Many organizations are stuck with outdated legacy systems...
  6. **Lack of Diversity and Inclusion**: The tech industry often struggles with diversity...
  7. **Data Overload**: Companies increasingly accumulate vast amounts of data...
  Each of these areas presents an opportunity for innovative solutions...
  ```
- **Explanation**: Lists multiple pain points, including cybersecurity threats, skill gaps, and legacy system integration, suitable for Agentic solutions.

### Propose a Solution
- **Purpose**: Requests a detailed Agentic AI solution for the top pain point, including tech stack and orchestration tools.
- **Code**:
  ```python
  # Ask it again ( this time with the  present a pain-point in that industry - something challenging that might be ripe for an Agentic solution)
  question = "Now can u propose a solution to the top painpoint based on revies etc from it professionals , a detailed solution with tech stack , orchestration tools and api is expected "
  messages = [{"role": "user", "content": question}]
  response = client.chat.completions.create(
      model="gpt-4o-mini",
      messages=messages
  )
  answer = response.choices[0].message.content
  print(answer)
  ```
- **Output**:
  ```markdown
  To propose a detailed solution to a top pain point identified by IT professionals, let's first identify a common pain point in the industry: **"Complexity in Managing Multi-Cloud Environments."**
  ### Proposed Solution: Unified Multi-Cloud Management Platform
  #### Overview
  The proposed solution is a Unified Multi-Cloud Management Platform that provides a centralized interface...
  #### Key Features
  1. **Centralized Dashboard**: A single pane of glass for monitoring resources...
  2. **Automated Deployment**: Streamlined provisioning and scaling...
  3. **Cross-Cloud Service Orchestration**: Manage workloads and services seamlessly...
  4. **Cost Management**: Real-time cost tracking...
  5. **Security Compliance**: Integrated security tools...
  ### Tech Stack
  1. **Frontend**: React or Angular, Tailwind CSS or Material-UI...
  2. **Backend**: Node.js or Python (Flask/FastAPI), PostgreSQL or MongoDB...
  3. **Container Orchestration**: Kubernetes, Helm...
  4. **Infrastructure as Code**: Terraform...
  5. **Monitoring & Observability**: Prometheus, Grafana, ELK Stack...
  6. **API Management**: AWS API Gateway or Kong...
  7. **Authentication & Authorization**: OAuth 2.0/OpenID Connect (Auth0 or Keycloak)...
  8. **CI/CD Tools**: Jenkins, GitHub Actions, or GitLab CI...
  ### Orchestration Tools
  1. **Service Mesh**: Istio or Linkerd...
  2. **Serverless Framework**: For deploying serverless functions...
  ### API Design
  1. **API Endpoints**:
     - `POST /api/projects`: Create a new project...
     - `GET /api/projects`: List all projects...
     - `POST /api/deployments`: Deploy an application...
     - `GET /api/metrics`: Fetch performance metrics...
     - `GET /api/costs`: Retrieve cost estimates...
  2. **Authentication**: Use OAuth2 for API calls...
  ### Implementation Steps
  1. **Requirement Gathering**: Collaborate with stakeholders...
  2. **Design Architecture**: Create a blueprint...
  3. **Develop MVP**: Build a Minimum Viable Product...
  4. **Testing**: Conduct unit, integration, and end-to-end testing...
  5. **Deployment**: Use CI/CD pipelines...
  6. **Feedback Loop**: Implement mechanisms for user feedback...
  7. **Documentation**: Provide comprehensive documentation...
  ### Conclusion
  This Unified Multi-Cloud Management Platform aims to mitigate the complexities...
  ```
- **Explanation**: Proposes a **Unified Multi-Cloud Management Platform** to address the pain point of managing multi-cloud environments, detailing features, tech stack, orchestration tools, API design, and implementation steps.

## Notebook Metadata
- **Kernel**: `.venv` (Python 3.12.5)
- **Language Info**:
  - Name: Python
  - Version: 3.12.5
  - File Extension: `.py`
  - Mimetype: `text/x-python`
  - CodeMirror Mode: `ipython`, version 3
  - Pygments Lexer: `ipython3`
- **Format**: Jupyter Notebook (nbformat 4, nbformat_minor 2)

## Summary
This notebook introduces users to Agentic AI by guiding them through environment setup, Azure OpenAI API interactions, and a practical exercise. It emphasizes hands-on learning with minimal reliance on high-level tools, focusing on foundational skills like environment variable management, API calls, and problem-solving with LLMs. The exercise encourages creative application of Agentic AI to real-world IT challenges, setting the stage for more advanced labs.
