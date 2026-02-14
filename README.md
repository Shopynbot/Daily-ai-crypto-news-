# Daily-ai-crypto-news-
Cryptocurrency news daily base on ai report
<!DOCTYPE html>
<html>
<head>
  <title>AI Crypto Daily Reporter</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      color: white;
      text-align: center;
      padding: 20px;
    }

    h1 {
      font-size: 26px;
      margin-bottom: 5px;
    }

    p {
      margin-bottom: 20px;
      font-size: 16px;
      opacity: 0.9;
    }

    .card {
      background: rgba(255,255,255,0.1);
      padding: 20px;
      border-radius: 12px;
      margin: 0 auto 20px auto;
      max-width: 450px;
      backdrop-filter: blur(8px);
      box-shadow: 0 6px 15px rgba(0,0,0,0.25);
    }

    button {
      background: #00ffcc;
      color: black;
      border: none;
      padding: 10px 18px;
      font-size: 15px;
      border-radius: 8px;
      cursor: pointer;
      margin-top: 10px;
      transition: 0.3s;
    }

    button:hover {
      background: #00ccaa;
    }

    .prices {
      font-size: 16px;
      margin-top: 15px;
      line-height: 1.5;
    }

    pre {
      text-align: left;
      white-space: pre-wrap;
      margin-top: 15px;
      font-size: 14px;
    }

    .footer {
      margin-top: 30px;
      font-size: 13px;
      opacity: 0.8;
    }
  </style>
</head>
<body>

  <h1>🚀 AI Crypto Daily Reporter</h1>
  <p>Live Prices + AI Market Summary</p>

  <div class="card">
    <button onclick="getCrypto()">Generate Today’s Report</button>

    <div class="prices" id="prices"></div>
    <pre id="output"></pre>
  </div>

  <div class="footer">✨ Made by Shopy</div>

<script>
async function getCrypto() {
  document.getElementById("output").innerText = "Loading AI report...";

  // Fetch crypto prices
  const priceRes = await fetch("https://api.coingecko.com/api/v3/simple/price?ids=bitcoin,ethereum,solana,near&vs_currencies=usd");
  const prices = await priceRes.json();

  // Display prices
  const priceText = `
Bitcoin: $${prices.bitcoin.usd}
Ethereum: $${prices.ethereum.usd}
Solana: $${prices.solana.usd}
NEAR: $${prices.near.usd}
`;
  document.getElementById("prices").innerText = priceText;

  // AI prompt
  const prompt = `
Bitcoin: $${prices.bitcoin.usd}
Ethereum: $${prices.ethereum.usd}
Solana: $${prices.solana.usd}
NEAR: $${prices.near.usd}

Give a short daily crypto market summary and simple advice.
`;

  // Call OpenAI API
  const aiRes = await fetch("https://api.openai.com/v1/chat/completions", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "Authorization": "Bearer YOUR_API_KEY_HERE"
    },
    body: JSON.stringify({
      model: "gpt-4o-mini",
      messages: [{ role: "user", content: prompt }]
    })
  });

  const aiData = await aiRes.json();
  document.getElementById("output").innerText =
    aiData.choices[0].message.content;
}
</script>

</body>
</html>
