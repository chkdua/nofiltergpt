
# NoFilterGPT API for JavaScript

The NoFilterGPT API for JavaScript provides developers with the ability to integrate the power of the NoFilterGPT AI model directly into web applications using JavaScript. This guide will cover the essentials to get you started, including setting up your API key, making API requests, and handling responses.

## Getting Your API Key

To begin using the NoFilterGPT API, you'll need an API key:
1. Log into your account at [nofiltergpt.com](https://nofiltergpt.com).
2. Navigate to the **"Settings"** page.
3. Click on the **"Developers"** tab.
4. Generate your API key.

## Setup

Include the following script in your HTML to start making API requests:

```html
<script>
    const apiKey = 'YOUR_API_KEY'; // Replace this with your actual API key
</script>
```

## How to Use the NoFilterGPT API

### Endpoint: `/v1/chat/completions`

This endpoint expects a **POST** request containing a JSON payload with your query.

### Required Parameters:

- **messages**: An array of message objects that represent the conversation. Each message must specify a role and content.
  
  Example:
  ```javascript
  messages: [
      { role: "system", content: "You are a helpful assistant." },
      { role: "user", content: "Hello! Can you help me with something?" }
  ]
  ```

### Optional Parameters:

- **temperature**: Controls the creativity of the responses. Default: `0.7`.
- **max_tokens**: Limits the number of tokens (words/subwords) in the response. Default varies by model.
- **top_p**: Controls diversity by filtering out less likely responses. Default: `1`.

### Making a Request:

Add the following JavaScript within your HTML file to interact with the API:

```javascript
document.getElementById('get-response').addEventListener('click', function() {
    const userInput = document.getElementById('user-input').value;
    if (!userInput.trim()) {
        alert("Please enter a question.");
        return;
    }

    const data = {
        messages: [
            { role: "system", content: "You are a helpful assistant." },
            { role: "user", content: userInput }
        ],
        temperature: 0.7,
        max_tokens: 150,
        top_p: 1
    };

    fetch(`https://api.nofiltergpt.com/v1/chat/completions?api_key=${apiKey}`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data)
    })
    .then(response => response.json())
    .then(data => {
        document.getElementById('response').innerText = JSON.stringify(data, null, 2);
    })
    .catch(error => {
        console.error('Error:', error);
        document.getElementById('response').innerText = 'Error fetching data';
    });
});
```

## Handling Responses

The API will respond with a completion or an error message, which should be handled accordingly in your application.

## Contributing

Contributions are welcome! If you have suggestions or improvements, feel free to fork the repository and submit a pull request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
