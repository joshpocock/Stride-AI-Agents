## Agent Workflows

## WebScraperAgent:

Purpose: To scrape and clean the content of a website provided by the user.

### Functionality:
Uses the scrape_website asynchronous function to fetch the website content.

Cleans the HTML content by removing scripts and styles using BeautifulSoup.

Extracts text and structures it for analysis.

Saves the full and extracted content to markdown files for later use.

## AnalystAgent:

Purpose: To analyze the scraped website content and provide key marketing insights.

### Functionality:

Utilizes the analyze_website_content function.

Sends the structured content to OpenAI's GPT model for analysis.

Generates insights that can inform marketing strategies based on the website's content.

## CampaignIdeaAgent:

Purpose: To create innovative campaign ideas based on the target audience and marketing goals specified by the user.

### Functionality:

Employs the create_campaign_idea function.

Takes user inputs for the target audience and goals.

Interacts with OpenAI's GPT model to generate a creative and strategic campaign idea.

## CopywriterAgent:

Purpose: To generate compelling marketing copy based on the campaign idea developed.

### Functionality:

Uses the generate_copy function.

Inputs the campaign idea into OpenAI's GPT model.

Produces marketing copy that aligns with the campaign's objectives and appeals to the target audience.

## UserInterfaceAgent:

Purpose: To manage user interactions and orchestrate the workflow between the different agents.

### Functionality:

Prompts the user for the website URL, target audience, and marketing goals.

Instantiates and coordinates the execution of the other agents in sequence:

Calls WebScraperAgent to scrape and prepare the website content.

Invokes AnalystAgent to analyze the content.

Uses CampaignIdeaAgent to generate a campaign idea based on user inputs.

Engages CopywriterAgent to create marketing copy from the campaign idea.

Displays messages to the user upon completion of the tasks.

## Workflow Summary:

Step 1: The user provides a URL, which WebScraperAgent processes to obtain and clean the website content.

Step 2: The cleaned content is analyzed by AnalystAgent to extract key marketing insights.

Step 3: The user specifies the target audience and marketing goals.

Step 4: CampaignIdeaAgent generates a campaign idea based on the provided information.

Step 5: CopywriterAgent creates marketing copy aligned with the campaign idea.

Step 6: The application concludes by thanking the user and provides information on how to implement AI agents into their business.