In Python 3.12, there's a change in how JSON serialization handles type objects. The problem is in how we're handling module settings.

I've modified the code to handle type objects in the settings by converting them to their string representation before JSON serialization. This change was necessary because:
- In Python 3.12, the JSON encoder is stricter about what it can serialize
- Type objects (like those that might be in module settings) cannot be directly serialized to JSON
- We now convert any type objects to their string names before serialization

The change specifically:
1. Captures the setting value in a variable
2. Checks if it's a type object using isinstance(value, type)
3. If it is a type, converts it to its string name using value.__name__
4. Otherwise uses the value as is
