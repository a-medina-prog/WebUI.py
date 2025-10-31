import openai
import os
import gradio as gr

openai.api_key = "sk-proj-UCf7Gh3Pq9Xa2ZLm4Rt6Yw8Nv0Bd5Kj1HrQeCsTuVoMiXpAzEnLbYcDgFkSjWhUoPlRaA"
openai.api_base = os.getenv("OPENAI_API_BASE")

messages = [
    {"role": "system", "content": "You are a financial expert that specializes in real estate investments."}
]

def CustomChatGPT(user_input):
    try:
        messages.append({"role": "user", "content": user_input})
        response = openai.ChatCompletion.create(
            model="gpt-3.5-turbo",
            messages=messages
        )

        ChatGPT_reply = response.choices[0].message["content"]
        messages.append({"role": "assistant", "content": ChatGPT_reply})
        return ChatGPT_reply
    except Exception as e:
        return f"Error: {str(e)}"
