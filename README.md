<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FinNav AI - Smart Financial Navigation Assistant</title>
    <meta name="description" content="FinNav AI - The smart financial assistant helping students and young adults make better money decisions through AI-powered chat conversations.">
    <meta name="keywords" content="FinNav AI, financial chatbot, money assistant, personal finance chatbot, budgeting AI, financial education bot, money management, student finance, AI chatbot">
    <meta name="author" content="FinNav AI Team">
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        :root {
            --primary-color: #4f46e5;
            --secondary-color: #f3f4f6;
            --accent-color: #10b981;
            --text-color: #1f2937;
            --light-text: #f9fafb;
        }
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f9fafb;
            color: var(--text-color);
            transition: all 0.3s ease;
        }
        
        .chat-container {
            max-width: 900px;
            height: 80vh;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 8px 10px -6px rgba(0, 0, 0, 0.1);
            border-radius: 16px;
            overflow: hidden;
            background-color: white;
            border: 1px solid #e5e7eb;
            transition: all 0.3s ease;
        }
        
        .chat-container:hover {
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.15);
        }
        
        .chat-header {
            background: linear-gradient(135deg, #2563eb 0%, #1e40af 100%);
            color: white;
            padding: 1.5rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        .chat-messages {
            height: calc(100% - 140px);
            overflow-y: auto;
            padding: 1rem;
            scrollbar-width: thin;
        }
        
        .message {
            max-width: 80%;
            margin-bottom: 1rem;
            padding: 0.75rem 1rem;
            border-radius: 1rem;
            line-height: 1.5;
            position: relative;
            word-wrap: break-word;
        }
        
        .user-message {
            background-color: var(--primary-color);
            color: white;
            margin-left: auto;
            border-bottom-right-radius: 0.25rem;
        }
        
        .bot-message {
            background-color: var(--secondary-color);
            color: var(--text-color);
            margin-right: auto;
            border-bottom-left-radius: 0.25rem;
        }
        
        .typing-indicator {
            display: inline-block;
            padding: 0.5rem 1rem;
            background-color: var(--secondary-color);
            border-radius: 1rem;
        }
        
        .typing-indicator span {
            display: inline-block;
            width: 8px;
            height: 8px;
            background-color: #9ca3af;
            border-radius: 50%;
            margin: 0 2px;
            animation: bounce 1.4s infinite ease-in-out;
        }
        
        .typing-indicator span:nth-child(2) {
            animation-delay: 0.2s;
        }
        
        .typing-indicator span:nth-child(3) {
            animation-delay: 0.4s;
        }
        
        @keyframes bounce {
            0%, 60%, 100% { transform: translateY(0); }
            30% { transform: translateY(-5px); }
        }
        
        .chat-input-container {
            padding: 1rem;
            border-top: 1px solid #e5e7eb;
            background-color: white;
        }
        
        .chat-input {
            width: 100%;
            padding: 0.75rem 1rem;
            border: 1px solid #e5e7eb;
            border-radius: 0.5rem;
            outline: none;
            transition: border-color 0.2s;
        }
        
        .chat-input:focus {
            border-color: var(--primary-color);
        }
        
        .send-button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 0.5rem;
            padding: 0.75rem 1.5rem;
            margin-left: 0.5rem;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        
        .send-button:hover {
            background-color: #4338ca;
        }
        
        .chat-icon {
            width: 40px;
            height: 40px;
            background-color: var(--accent-color);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            margin-right: 1rem;
        }
        
        .powered-by {
            font-size: 0.75rem;
            color: #6b7280;
            text-align: center;
            margin-top: 0.5rem;
        }
        
        .webchat-iframe {
            width: 100%;
            height: 100%;
            border: none;
            border-radius: 0 0 12px 12px;
        }
        
        @media (max-width: 640px) {
            .chat-container {
                height: 90vh;
            }
            
            .message {
                max-width: 90%;
            }
        }
    </style>
</head>
<body class="flex flex-col items-center justify-center min-h-screen p-4 bg-gray-50">
    <div class="w-full max-w-4xl text-center mb-8">
        <h1 class="text-4xl font-bold text-gray-800 mb-3 bg-gradient-to-r from-teal-600 to-emerald-600 bg-clip-text text-transparent">
            <span class="text-emerald-600">FinNav</span> <span class="text-teal-500">AI</span> <span class="text-lg text-gray-500">| Financial Education Assistant</span>
        </h1>
        <p class="text-lg text-gray-600 max-w-2xl mx-auto">
            Your AI-powered financial mentor - Learn money management through natural conversations
        </p>
    </div>
    
    <div class="chat-container w-full">
        <div class="chat-header">
            <div class="flex items-center space-x-3">
                <div class="chat-icon">
                    <svg xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
                        <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"></path>
                    </svg>
                </div>
                <div class="h-8 w-0.5 bg-white/20"></div>
            </div>
            <div>
                <h2 class="text-xl font-semibold">FinNav AI Assistant</h2>
                <p class="text-sm opacity-80">
                    <span class="inline-block w-2 h-2 rounded-full bg-green-400 mr-1"></span> 
                    Available 24/7
                </p>
            </div>
        </div>
        
        <iframe class="webchat-iframe" src="https://cdn.botpress.cloud/webchat/v3.0/shareable.html?configUrl=https://files.bpcontent.cloud/2025/05/09/05/20250509055350-QZUO5N9T.json"></iframe>
    </div>
    
    <div class="mt-6 text-center">
        <p class="text-sm text-gray-500">
            Secured with end-to-end encryption • GDPR compliant
        </p>
        <p class="powered-by mt-1">
            <strong>FinNav AI</strong> • <span class="text-emerald-600">Trusted Financial Chatbot</span> • Powered by Advanced AI
        </p>
    </div>

    <script>
        // If you want to add any custom JavaScript functionality
        document.addEventListener('DOMContentLoaded', function() {
            // This is where you could add additional interactivity
            // For full control, you'd typically use the Botpress SDK
            // But the iframe integration works well for quick deployment
        });
    </script>
</body>
</html>
