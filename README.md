
# 🚀 First AI LLM Prompts with OpenAI and LangChain  

This project demonstrates how to use **OpenAI’s API** with **LangChain** to generate AI-powered responses based on structured prompt templates. The main objective is to generate a **Major League Baseball (MLB) expansion team name** based on a given city and primary color.  

## 📌 Project Overview  
- **Integrates OpenAI's GPT model with LangChain**  
- **Uses prompt templates for structured text generation**  
- **Implements LLMChains for AI-driven automation**  
- **Saves and loads prompt templates for reuse**  

---

## 🛠️ Installation  

Ensure you have Python installed, then install the required dependencies:  

```bash
pip install openai langchain langchain-community
```

Set up your **OpenAI API Key**:  

```python
import os
os.environ["OPENAI_API_KEY"] = "YOUR_API_KEY"
```

---

## 📖 Usage  

### 1️⃣ **Initializing OpenAI’s Model**  

```python
from langchain.llms import OpenAI

llm = OpenAI(temperature=0.9, openai_api_key=os.environ["OPENAI_API_KEY"])

text = "Create a baseball team name that would be great for MLB Expansion"
print(llm(text))
```
✅ **Temperature = 0.9** ensures creative responses.  

---

### 2️⃣ **Using Prompt Templates**  

A **PromptTemplate** is created for structured input:  

```python
from langchain.prompts import PromptTemplate

prompt_template_baseball_team = PromptTemplate(
    input_variable=["city,colour"],
    template="Create a baseball team name that would be great for MLB Expansion in {city} with primary colour {colour}"
)

print(llm(prompt_template_baseball_team.format(city="Chicago", colour="Red")))
```

---

### 3️⃣ **Saving & Loading Prompt Templates**  

#### **Save the template to a file**  
```python
prompt_template_baseball_team.save("prompt_template_baseball_team.json")
```

#### **Load the saved template**  
```python
from langchain.prompts import load_prompt

loaded_prompt = load_prompt("prompt_template_baseball_team.json")
print(loaded_prompt.format(city="Chicago", colour="Red"))
```

---

### 4️⃣ **Building an AI Chain with LangChain**  

A function is created to integrate **LLMChain** for automation:  

```python
from langchain.chains import LLMChain

def generate_baseball_team_name(city, colour):
    llm = OpenAI(temperature=0.9)

    prompt_template_baseball_team = PromptTemplate(
        input_variable=["city,colour"],
        template="Create a baseball team name that would be great for MLB Expansion in {city} with primary colour {colour}"
    )

    baseballchain = LLMChain(llm=llm, prompt=prompt_template_baseball_team)
    response = baseballchain({"city": city, "colour": colour})

    return response["text"]

print(generate_baseball_team_name("Chicago", "Red"))
```

This function:  
✔ Creates an **LLMChain**  
✔ Uses the prompt template for structured input  
✔ Returns an **MLB expansion team name** dynamically  

---

## 🔄 Future Improvements  

✅ Fine-tune prompt engineering for optimized results  
✅ Implement LangChain memory for conversation history  
✅ Deploy as an interactive web app using **Streamlit**  

---

## 📜 License  

This project is licensed under the **MIT License**.  

---

## 🎯 Contributing  

🚀 Feel free to submit **issues** and **pull requests**! Let's build something awesome together.  


