# Environment setup

Create a `.env` file in the project root (the same folder as `pyproject.toml`),
and add your Groq API key:

```dotenv
GROQ_API_KEY=your_groq_api_key
```

The notebook loads this file with `python-dotenv`. Keep `.env` local; it is
ignored by Git. `.env.example` shows the required variable name without a real
key.