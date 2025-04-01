# Appancyster

## Custom Text Encryption Framework

Appancyster is a custom text encryption tool that implements multi-round substitution with deterministic noise injection to protect sensitive information.

## Features

- **Multi-round Character Substitution**:
  - Uses configurable substitution rounds (default: 3 rounds)
  - Custom character mapping for each round
  - Supports Latin, Cyrillic, numeric, and symbol characters

- **Salt-based Encryption**:
  - Generates random salt for each encryption
  - Salt preserved in output for decryption
  - Deterministic random seed based on salt

- **Noise Injection**:
  - Strategically inserts noise characters at predictable positions
  - Noise characters determined by salt value
  - Deterministic insertion pattern for reliable decryption

- **Persistent Encryption Keys**:
  - Stores substitution maps in JSON file
  - Maintains encryption/decryption consistency
  - Option to regenerate keys when needed

## How It Works

The encryption process follows these steps:

1. **Salt Generation**: Creates a random alphanumeric salt
2. **Multi-round Substitution**: Applies character substitution across multiple rounds
3. **Noise Injection**: Inserts deterministic noise characters every 3rd position
4. **Formatting**: Combines salt with encrypted text using a separator (salt|encrypted_text)

The decryption process reverses these steps:

1. **Format Parsing**: Extracts salt and encrypted content
2. **Noise Removal**: Strips out the noise characters based on pattern
3. **Reverse Substitution**: Applies character substitution maps in reverse order

## Example Encryption

### Original Text:
```
Hello World! This is a secret message.
```

### Encrypted Result:
```
AbCd1234|Пщ~ФЫо@ЯхЙ%з!_ЪфИс$_ЦЧкщ^_Ы_Э?жНчАю~_БлЫсщй&жк_
```

In this example:
- `AbCd1234` is the random salt
- `|` is the separator
- The remaining text contains both substituted characters and injected noise
- Every third character position has a noise character inserted
- Spaces are replaced with underscores

## Character Set

Appancyster uses an extensive character set including:
- Latin characters (a-z, A-Z)
- Cyrillic characters (А-Я, а-я)
- Numeric digits (0-9)
- Special symbols

## Implementation

The framework requires Python 3 and uses only standard library modules:
- `random`: For salt generation and deterministic noise
- `json`: For storing and reading encryption keys
- `os`: For file operations
- `time`: For timestamp tracking

## Usage

```python
# Create an Appancyster instance
crypto = Appancyster()

# Encrypt text
encrypted = crypto.encrypt("Your secret message")

# Decrypt text
decrypted = crypto.decrypt(encrypted)
```

## Created By

Dava Yuste - Spiuwirkid
