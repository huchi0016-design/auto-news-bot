import requests
import json

# ===== ဒီနေရာမှာ ခင်ဗျားရဲ့ API Key ကို ထည့်ပါ =====
from secrets import API_KEY
import requests
import json
GEMINI_URL = f"https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key={API_KEY}"

print("=== 🧠 Huchika Agent (Gemini AI ဗားရှင်း) ===")
print("ဘာမေးမေးဖြေနိုင်ပါပြီ။ (ထွက်ချင်ရင် 'ထွက်' လို့ရိုက်ပါ)")
print("------------------------------------------------")

def ask_gemini(question):
    """Gemini AI ကို မေးခွန်းမေးပြီး အဖြေရယူတယ်"""
    payload = {
        "contents": [{
            "parts": [{"text": question}]
        }]
    }
    headers = {"Content-Type": "application/json"}
    
    try:
        response = requests.post(GEMINI_URL, json=payload, headers=headers)
        data = response.json()
        
        # Gemini ရဲ့ အဖြေကို ထုတ်ယူတယ်
        answer = data["candidates"][0]["content"]["parts"][0]["text"]
        return answer
    except Exception as e:
        return f"AI ကို ဆက်သွယ်ရာမှာ အမှားရှိနေတယ်။ Error: {e}"

# စကားပြောစက်ဝိုင်း (Loop)
while True:
    user_input = input("သင့်မေးခွန်း: ")
    
    if user_input == "ထွက်":
        print("Huchika Agent: နောက်မှပြန်တွေ့မယ်။ ကျေးဇူးပါ။ 👋")
        break
    
    # Gemini AI ကို မေးခွန်းပို့ပြီး အဖြေယူမယ်
    print("Huchika Agent: ", end="")
    reply = ask_gemini(user_input)
    print(reply)
    print("------------------------------------------------")
