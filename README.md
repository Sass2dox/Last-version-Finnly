# Last-version-Finnly
last version
<img width="248" alt="image" src="https://github.com/user-attachments/assets/2d3c10d9-8fab-4fc8-94ef-bdb31a5c5bfe" />


# FINLEY — Personal Finance Assistant for Teenagers

## 📱 Project Description:
Finley is an iOS application that helps teenagers manage their finances: plan weekly budgets, track expenses, save for goals, and receive advice from an AI assistant. It also includes a parent control feature—parents can view activity but cannot interfere with financial decisions.

The app is developed using Swift and SwiftUI in Xcode. This is an individual project created for Technovation.

---

## 🧠 OpenAI Integration:
The AI assistant uses the OpenAI GPT model (via API) to:
- analyze user-provided data (expenses, goals);
- generate personalized financial advice;
- help teenagers make informed budget decisions.

### ⚠️ Temporarily Disabled:
Due to limitations with the paid OpenAI API key, the AI functionality is temporarily unavailable. However:
- All integration code with OpenAI is fully preserved.
- The logic has been implemented and tested.
- A sample request is shown below.

---

## ⚙️ How AI Integration Works:

1. The user inputs expenses and a savings goal.
2. This data is serialized into a text prompt.
3. The prompt is sent to the OpenAI API.
4. The response (advice) is shown on screen as a suggestion.

Sample code:
```swift
func sendToOpenAI(prompt: String, completion: @escaping (String) -> Void) {
    let url = URL(string: "https://api.openai.com/v1/completions")!
    var request = URLRequest(url: url)
    request.httpMethod = "POST"
    request.setValue("Bearer YOUR_API_KEY", forHTTPHeaderField: "Authorization")
    request.setValue("application/json", forHTTPHeaderField: "Content-Type")
    
    let parameters: [String: Any] = [
        "model": "text-davinci-003",
        "prompt": prompt,
        "max_tokens": 150
    ]
    request.httpBody = try? JSONSerialization.data(withJSONObject: parameters)

    URLSession.shared.dataTask(with: request) { data, _, _ in
        if let data = data,
           let response = try? JSONSerialization.jsonObject(with: data) as? [String: Any],
           let choices = response["choices"] as? [[String: Any]],
           let result = choices.first?["text"] as? String {
            DispatchQueue.main.async {
                completion(result.trimmingCharacters(in: .whitespacesAndNewlines))
            }
        }
    }.resume()
}
```

---

## 👪 Parent Control:
- A separate “Parent Mode” section is available.
- Parents can see activity logs and expenses but cannot modify them.
- Protected by a password or PIN.

---

## 📁 How to Open the Project:
1. Unzip the archive and open `Finley.xcodeproj` in Xcode.
2. Make sure you have SwiftUI (Xcode 14.0 or later).
3. Run the app on a simulator or physical device.

---

## 💻 Technologies Used:
- Swift + SwiftUI
- OpenAI API (GPT-3.5)
- UserDefaults (for local data storage)
- UIKit (some components)
- MVVM Architecture

---

## 👩‍💻 What I Implemented:
- Full UI/UX design and layout.
- Financial logic: budget planning, goal tracking, and expenses.
- OpenAI integration via REST API.
- Parent control functionality.
- App testing and deployment.

---

## 📝 Additional Info:
- A demo key can be added later 
