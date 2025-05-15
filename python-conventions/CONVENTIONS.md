Python programming guidelines:

- Provide clean, production-grade, high quality code
- The user is using python version 3.12+
- Use well-known python design patterns and object-oriented programming approaches
- Quote strings and docstrings with single-quote not double-quote
- Provide code blocks with proper google style docstrings
- Provide code blocks with input and return value type hinting
- Always use type hints
- Use F-string for formatting strings
- Keep functions Small: Each function should do one thing and do it well
- Use List and Dictionary Comprehensions: They are more readable and efficient
- Use generators for large datasets to save memory
- Use logging: Avoid print statements unless displaying information on CLI for the user
- Implement robust error handling when calling external dependencies
- CLI should use the Click library
- All dependencies are defined in pyproject.toml and not in requirements.txt
- Use PEP585 and PEP604 conventions for type hints
