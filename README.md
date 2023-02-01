### Hi there 👋

<!--
**SirHung/sirhung** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
import os
import openai
import gradio as gr
from pyChatGPT import ChatGPT

session_token = "eyJhbGciOiJkaXIiLCJlbmMiOiJBMjU2R0NNIn0..91k-A1E8czlLfoPK.tKl8XfXoZMM813PfUnDd8y5URWT-Wu_4RctTXJfwUMLUHoM29R82YyMbc7aLl9bSy8G-f0m-0S3wqPnSKpJlDIyFw1paHgBIVk6Dp-7RSeV_r2PGOYxN5AIAKZTH91d4xmh1oESFkSdou-H__lg7QmvJVhhYTnbcqpYEpgPojof_B0UdeQGpaTg6hWMv0loJN_HK9Kpg4hflg08NCWUSLtcH-3cnsgHsATGUXOS-PviLqWKtnY2vtaJlddTFYvSMNwPKqc-wgbt9dJ-IExvMEz_siJ_-ju9CUSn8L46QfKyS80CWxshgVN2Mxaxa5UPhzHicP1rMgg-cUvzhMBzn3a7WUwbZQDGcI9boTovf2z9ACamPsXQmi5lkrUHFTtPijXq0ZKS5Ryk_E2rn-ZJSxxP9CbZTfBIarW_gmaveC_eO1Q-uXIAwYkjD6IU9_o-uuVnO7sr30UBP0QOStSgdHY2691MazPFZr5kWctIuKWEyPU4AH5eQ9deevvFe6CpWwqEFgv0W2AL3h2uSisKJXCSDUpZx4HR97enJVG1psHhNuANSlRUTHm7yqM7YJ8rLotl6zw4dE8S-RihlMHQB4JWjHx-11RvJp2N3zBUZ5lrlmO1KQ7In5j6pgjDZcGj3KHm9-l111VZ9iIYD79taJoonAXTTmyFUXmHz7ioYRviSFoAVFs-tFNiQCZeLI_wk-0VUMCb5XHDKVqMcPJVxO3EYgIjr3ih_ZVEBhF0oHXqnfRmmPCjsXqIPxTQGbJjGp-D-9msCMem87rBxUeWfhCKfoipTESCrVlEX9c_ep2RGqckuB6hdQf3fCCdrgmXtAnyVBsauTTpiskCo8j2OZBQLVBmY3F0Fnhoh-3xhHg88_ud-lagYULkDcszrmxJlKpRk__Vw7QJicfY5YN-iKyml6g_WkZvEceWAS1qGRLDkypSSsl31_c-PyIkrUAjg_QeM7IG-rL4zU32mvGomL-dgnSVdn7vrLCNzfAfsIo30m8YLUtVMjtTTATiitanUH8CLYcStnmjedEsUcZo240RfCvyUROrIrqtK0B90ZVRPEA8wxOJrj4YeIZZcjs24ePz3FAwbBy5y16ZcNiaomonSEG6s0KCPzU4SYhjQznkq80PDRdEP_3xWNs_QbSU2mgpea1tcYTtfcBgkwLpeJFbLyXSCWNP1vQKMk8uKhg_v_KWqXeexf9kDR4TUqGOagj7RYokUue_AYMr_qmUmKFbEXx33vX8k50_9PGR9XtOxOTQuZyJoYltCWy6xhk4HAgC0_eJC7VeLBLrVNZ9z8BxuKEQJX5iLN0bugcIUf3NxJ2B1cIO5y9tjiRHQwOFttx_91AHIlrbLxoi0MeVmZmo3SlqBY3-FduoAxmkOtQwjtCZKOENNFO0WT4vB6fyeCJf5-myNPrscKuXwCzhUh0tRSMzCBiNgcXedj-jYX3Td_M2GUeodOfDa3nx2MymsvegRvmGTqgZINclzzp1PyBclViAG6uNNRzxUFKNqq76cCdrt6T_uvAEwhAPiexebXwwX2g9rdUJJsFW65icK1Bb29IBBmbtAYoYaPZf-pWSZgAuGgwZbkuu1_UctUop2btezi-EheOAqdJVcqR1zJeA_-JQ-qQD-uHYoNTwk0bXWGzktb6P6gr-LOVFBgU7IhFlMBWM0P_lq02Czc3Rd0tJRlyTg6_NBSRZWtAsc6n5yZF_XWf-rJ0G1AQhHsTmeyyNO96on3AIDEy3JGHTRNjbtKU_EUwf1SkGMyUFkyXGDTTKMGxPCKeC5shuQXg-fHs_lE1HHKU4PZlfPs43LHgbeATkSEcJUJ-JfdISQtLugPi12MZ-jihMn2IKbKoNPWC9OUF4KmngCT0ykVgzvAarAgwKse1y8IjHwr9VFjjm-nCpwjEGRGKEWsCBpFRlhLzS3EmsbCMtHWc8bP7Kv6nWPeFj-z1s3DXwlHUwR-7racn87W9J59ehDmK4FZiTa_Z9DPhVkACTaPsrZc5NRUuBoAW9BUbzaGckp9bY4prI0SYyjvWo8awUnjD2obHtUWRf34AVqroLkzqMYd4lpfZJDdS0dzK4sNqssEM21-ydwag4DPpiMmfPk2zP7tygJPUcyLgzC1isZfmUvFnVqHMcZkWykUBuNCbVo-hv8kLr06dXILJbdwu8xma8EIbsOtKh6fasNiU28tFc4OuFR93hbyrvyqDfuu-sS2-uXFPpfzWkGqs9yzoa3RkJJbJLgSsELicd_hw0v4zknv7-FyEnP6D45Eb4DfE2Sk4BMXQRrmWq1bv3EGJe87BToX3dOwNzMVyWXjDDeDAAPXqWSPr115p1NWumkGeh5dz8fRfXr-NoXjEdyOe5eX3-yi58BnVONmlP1we30y8Na_I5aZZrjAgdyOzXJOJ_K_UvWIG5I0LQzA26jp1Eo1K4n2Kq_i0_zvcD9oCBfn5hTTaRKNXxd8sLiZRrx1gy0iOC-7VxUFCmPDkoo4lELLWADDbxJE6N1bNeVd6uWPbiFC-VPIR9K1AnMyspZvbMwI2wMmjM9GqhydysZzYJw9WXVvaX8O2hQRQcINEgfJAHDIhCRM4g5u4vVVA_B6qS_7haGb1S9ZxR2XGqRfEEMm9R7-ilq5OseO1GuZVlXKVghJyQUksBO0bnmDcDxYTgoFaCHy3lxmlBJE7PttbmzxP9J9hz4tSzImLxBvVJjt9qd.JAnrume8TxHqZc9_MCd6Vg"



start_sequence = "\nAI:"
restart_sequence = "\nHuman: "

prompt = "The following is a conversation with an AI assistant. The assistant is helpful, creative, clever, and very friendly.\n\nHuman: Hello, who are you?\nAI: I am an AI created by OpenAI. How can I help you today?\nHuman: "

def openai_create(prompt):

    response = openai.Completion.create(
    model="text-davinci-003",
    prompt=prompt,
    temperature=0.9,
    max_tokens=150,
    top_p=1,
    frequency_penalty=0,
    presence_penalty=0.6,
    stop=[" Human:", " AI:"]
    )

    return response.choices[0].text



def chatgpt_clone(input, history):
    history = history or []
    s = list(sum(history, ()))
    s.append(input)
    inp = ' '.join(s)
    output = openai_create(inp)
    history.append((input, output))
    return history, history

def outputsGPT(input, history):
    resp = api1.send_message(input)
    history = history or []
    s = list(sum(history, ()))
    s.append(input)
    output = resp['message']
    history.append((input, output))
    print("Human: ", input)
    print("ChatGPT: ", output)
    return history, history


block = gr.Blocks()
api1 = ChatGPT(session_token) 

with block:
    try:
        chatbot = gr.Chatbot()
        message = gr.Textbox(placeholder=prompt)
        state = gr.State()
        submit = gr.Button("SEND")
        submit.click(outputsGPT, inputs=[message, state], outputs=[chatbot, state])
    except Exception as e:
        print("Error: ", e.message, e.args)

block.launch(debug = False, show_api=False)import os
import openai
import gradio as gr
from pyChatGPT import ChatGPT

session_token = "Token"



start_sequence = "\nAI:"
restart_sequence = "\nHuman: "

prompt = "The following is a conversation with an AI assistant. The assistant is helpful, creative, clever, and very friendly.\n\nHuman: Hello, who are you?\nAI: I am an AI created by OpenAI. How can I help you today?\nHuman: "

def openai_create(prompt):

    response = openai.Completion.create(
    model="text-davinci-003",
    prompt=prompt,
    temperature=0.9,
    max_tokens=150,
    top_p=1,
    frequency_penalty=0,
    presence_penalty=0.6,
    stop=[" Human:", " AI:"]
    )

    return response.choices[0].text



def chatgpt_clone(input, history):
    history = history or []
    s = list(sum(history, ()))
    s.append(input)
    inp = ' '.join(s)
    output = openai_create(inp)
    history.append((input, output))
    return history, history

def outputsGPT(input, history):
    resp = api1.send_message(input)
    history = history or []
    s = list(sum(history, ()))
    s.append(input)
    output = resp['message']
    history.append((input, output))
    print("Human: ", input)
    print("ChatGPT: ", output)
    return history, history


block = gr.Blocks()
api1 = ChatGPT(session_token) 

with block:
    try:
        chatbot = gr.Chatbot()
        message = gr.Textbox(placeholder=prompt)
        state = gr.State()
        submit = gr.Button("SEND")
        submit.click(outputsGPT, inputs=[message, state], outputs=[chatbot, state])
    except Exception as e:
        print("Error: ", e.message, e.args)

block.launch(debug = False, show_api=False)
