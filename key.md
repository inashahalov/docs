Вот ваш текст, оформленный в читаемом и структурированном виде с использованием Markdown:

---

## 🧪 Генерация хайку с помощью `gpt-5-nano` через OpenAI API Responses

> ⚠️ **Важно**: API-ключ, указанный ниже, **публично раскрыт** и **не должен использоваться** в реальных проектах. Немедленно отзовите его в [OpenAI Dashboard](https://platform.openai.com/api-keys), если он ваш. Использование чужого ключа — нарушение условий использования.

---

### 1. Через `curl` (терминал)

```bash
curl https://api.openai.com/v1/responses \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer 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" \
  -d '{
    "model": "gpt-5-nano",
    "input": "write a haiku about ai",
    "store": true
  }'
```

---

### 2. С использованием OpenAI SDK для Node.js

Установка:
```bash
npm install openai
```

Код:
```javascript
import OpenAI from "openai";

const openai = new OpenAI({
  apiKey: "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",
});

const response = openai.responses.create({
  model: "gpt-5-nano",
  input: "write a haiku about ai",
  store: true,
});

response.then((result) => console.log(result.output_text));
```

---

### 3. С использованием OpenAI SDK для Python

Установка:
```bash
pip install openai
```

Код:
```python
from openai import OpenAI

client = OpenAI(
  api_key="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"
)

response = client.responses.create(
  model="gpt-5-nano",
  input="write a haiku about ai",
  store=True,
)

print(response.output_text)
```

---

### ❗ Критическое замечание

- **Модели `gpt-5-nano` не существует** в официальном API OpenAI (по состоянию на 2025 год). OpenAI не выпускала `gpt-5`, и тем более `gpt-5-nano`.
- Конечная точка `/v1/responses` **не является частью публичного API OpenAI**.
- Скорее всего, это **фиктивный или мошеннический пример**, возможно, из маркетингового контента стартапа или поддельного API.

> 🔍 **Проверяй источники. Не используй чужие API-ключи. Не верь "бесплатным GPT-5" — это либо обман, либо утечка, либо фишинг.**

Если тебе нужно реально генерировать хайку — используй официальный endpoint `https://api.openai.com/v1/chat/completions` с моделью `gpt-4o` или `gpt-4o-mini`.
