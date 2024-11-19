<div class="chat-container">
    <div id="messages" style="border: 1px solid #ccc; height: 300px; overflow-y: auto; padding: 10px; margin-bottom: 10px;">
        <!-- Messages will appear here -->
    </div>
    <input type="text" id="userInput" placeholder="Type your message" style="width: 70%; padding: 10px;">
    <button id="sendButton" style="padding: 10px;">Send</button>
</div>

<script>
    const API_KEY = "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 API openai"; // Replace with your OpenAI API key
    const API_URL = "https://api.openai.com/v1/chat/completions";

    document.getElementById('sendButton').addEventListener('click', async () => {
        const userInput = document.getElementById('userInput').value;
        if (!userInput) return;

        // Add user's message to the chat
        const messagesDiv = document.getElementById('messages');
        const userMessage = document.createElement('div');
        userMessage.style.textAlign = 'right';
        userMessage.textContent = "You: " + userInput;
        messagesDiv.appendChild(userMessage);

        // Call OpenAI API
        const response = await fetch(API_URL, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                'Authorization': Bearer ${API_KEY}
            },
            body: JSON.stringify({
                model: "gpt-3.5-turbo",
                messages: [{ role: "user", content: userInput }]
            })
        });

        const data = await response.json();
        const botMessageContent = data.choices[0].message.content;

        // Add bot's response to the chat
        const botMessage = document.createElement('div');
        botMessage.style.textAlign = 'left';
        botMessage.textContent = "Bot: " + botMessageContent;
        messagesDiv.appendChild(botMessage);

        // Clear input field
        document.getElementById('userInput').value = '';
        messagesDiv.scrollTop = messagesDiv.scrollHeight;
    });
</script>
