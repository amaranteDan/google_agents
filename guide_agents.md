## How to Use ADK - Agent DEvelopment Kit 
- Reference: https://google.github.io/adk-docs/get-started/python/

Installation¶
Install ADK by running the following command:

pip install google-adk

Create an agent project¶
Run the adk create command to start a new agent project.

adk create my_agent

Explore the agent project¶
The created agent project has the following structure, with the agent.py file containing the main control code for the agent.

my_agent/
    agent.py      # main agent code
    .env          # API keys or project IDs
    __init__.py

Update your agent project¶
The agent.py file contains a root_agent definition which is the only required element of an ADK agent. You can also define tools for the agent to use. Update the generated agent.py code to include a get_current_time tool for use by the agent, as shown in the following code:

from google.adk.agents.llm_agent import Agent

# Mock tool implementation
def get_current_time(city: str) -> dict:
    """Returns the current time in a specified city."""
    return {"status": "success", "city": city, "time": "10:30 AM"}

root_agent = Agent(
    model='gemini-2.5-flash',
    name='root_agent',
    description="Tells the current time in a specified city.",
    instruction="You are a helpful assistant that tells the current time in cities. Use the 'get_current_time' tool for this purpose.",
    tools=[get_current_time],
)

Set your API key¶
This project uses the Gemini API, which requires an API key. If you don't already have Gemini API key, create a key in Google AI Studio on the API Keys page.

In a terminal window, write your API key into an .env file as an environment variable:

echo 'GOOGLE_API_KEY="YOUR_API_KEY"' > .env

Run your agent¶
You can run your ADK agent with an interactive command-line interface using the adk run command or the ADK web user interface provided by the ADK using the adk web command. Both these options allow you to test and interact with your agent.

Run with command-line interface¶
Run your agent using the adk run command-line tool.

adk run my_agent

Run with web interface¶
The ADK framework provides web interface you can use to test and interact with your agent. You can start the web interface using the following command:

adk web --port 8000

Note

Run this command from the parent directory that contains your my_agent/ folder. For example, if your agent is inside agents/my_agent/, run adk web from the agents/ directory.


