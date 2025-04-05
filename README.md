# GenAI-security
Securing AI Systems themselves
import gradio as gr
import openai
openai.api_key ="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"
def check_prompt_safety(prompt):
    try:
        response = openai.ChatCompletion.create(
            model="gpt-3.5-turbo",
            messages=[
                {"role": "system", "content": "You are a security assistant. Respond only with 'Safe' or 'Unsafe'."},
                {"role": "user", "content": f"Is this prompt safe?\n\n{prompt}"} ],
            temperature=0
        )
        result = response.choices[0].message["content"].strip()
        return f"🛡️ Result: {result}"
    except Exception as e:
        return f"❌ Error: {e}"
gr.Interface(
    fn=check_prompt_safety,
    inputs=gr.Textbox(lines=4, label="Enter your AI Prompt"),
    outputs="text",
    title="🔐 GenAI Prompt Safety Checker",
    description="This tool checks if a user prompt is safe or potentially harmful.",
).launch()
