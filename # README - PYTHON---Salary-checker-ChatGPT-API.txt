CHATGPT CONVERSATION

*********************

create a PYTHON code (with CHATGPT API) that checks the average salary for any position 


ChatGPT said:
Here's a Python script that uses the OpenAI ChatGPT API to check the average salary for any position by querying the web. It integrates OpenAI's API with a web search function to fetch salary data.

Salary Checker

Answer in chat instead
This script:

Queries a web search engine for salary data.

Uses ChatGPT to estimate the salary.

Combines both sources for a more reliable answer.

You'll need to replace "YOUR_OPENAI_API_KEY" with your actual OpenAI API key. Would you like any modifications? 🚀

*********************

import openai
import requests

def get_salary_data(job_title, location="Hungary"):
    search_query = f"average salary for {job_title} in {location}"
    search_url = f"https://api.duckduckgo.com/?q={search_query}&format=json"
    
    response = requests.get(search_url)
    data = response.json()
    
    if "AbstractText" in data and data["AbstractText"]:
        return data["AbstractText"]
    else:
        return "Salary data not found. Try refining your search."

def ask_chatgpt(query):
    openai.api_key = "YOUR_OPENAI_API_KEY"
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "system", "content": "You are a helpful assistant."},
                  {"role": "user", "content": query}]
    )
    return response["choices"][0]["message"]["content"]

def get_average_salary(job_title, location="Hungary"):
    web_result = get_salary_data(job_title, location)
    chatgpt_result = ask_chatgpt(f"What is the average salary for a {job_title} in {location}?")
    
    return f"Web Data: {web_result}\n\nChatGPT Data: {chatgpt_result}"

if __name__ == "__main__":
    job_title = input("Enter job title: ")
    location = input("Enter location (default: Hungary): ") or "Hungary"
    
    salary_info = get_average_salary(job_title, location)
    print(salary_info)
