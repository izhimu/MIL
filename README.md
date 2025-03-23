# MIL
A compact and efficient Model Interaction Language

## Target

The goal is to become a data interaction language between LLMs and between humans and LLMs. It is primarily characterized by compactness and efficiency, while maintaining a certain degree of interpretability and readability.

## Example

- Readable format

```
name=get_current_weather
description=Get the current weather in a given location
parameters{
    type=object
    properties{
        location{
            type=string
            description="The city and state, e.g. San Francisco, CA"
        }
        unit{
            type=string
            enum=celsius,fahrenheit
            description="The unit of temperature, either 'celsius' or 'fahrenheit'"
        }
    }
    required=location
}
```

> Compare json format
> 
> MIL tokens is **106**, JSON tokens is **151**, Can reduce **45** tokens, Decline **29.8%**.

``` json
{
    "name": "get_current_weather",
    "description": "Get the current weather in a given location",
    "parameters": {
        "type": "object",
        "properties": {
            "location": {
                "type": "string",
                "description": "The city and state, e.g. San Francisco, CA"
            },
            "unit": {
                "type": "string",
                "enum": [
                    "celsius",
                    "fahrenheit"
                ],
                "description": "The unit of temperature, either 'celsius' or 'fahrenheit'"
            }
        },
        "required": [
            "location"
        ]
    }
}
```

- Compression format

```
name=get_current_weather description=Get the current weather in a given location parameters{type=object properties{location{type=string description="The city and state, e.g. San Francisco, CA"}unit{type=string enum=celsius,fahrenheit description="The unit of temperature, either 'celsius' or 'fahrenheit'"}}required=location}
```

> Compare json format
> MIL tokens is **84**, JSON tokens is **96**, Can reduce **12** tokens, Decline **12.5%**.

``` json
{"name":"get_current_weather","description":"Get the current weather in a given location","parameters":{"type":"object","properties":{"location":{"type":"string","description":"The city and state, e.g. San Francisco, CA"},"unit":{"type":"string","enum":["celsius","fahrenheit"],"description":"The unit of temperature, either 'celsius' or 'fahrenheit'"}},"required":["location"]}}
```

## Roadmap

Planned language features:

- General LLM Prompt

    Provides prompts for all types of LLM to use MIL normally.

- Structural Description

    Add a general data structure definition description to the data header to inform LLM how to use this data and the meaning of each field.

- Path reference

    Data that already exists in the model context can be referenced to further save tokens.

- Binary Compression

    Based on MessagePack, the data volume is further compressed and can be used in scenarios such as network transmission.

Programming language support:

- Python
- Java
- Javascript
- Rust
- ...

Structural conversion:

- JSON
- TOML
- YAML

