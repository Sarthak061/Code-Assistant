# AI-Assisted Code Implementation and Verification Tool

## Overview
This project provides a command-line tool that utilizes a pre-trained language model (Llama-3.2-1B-Instruct) to assist developers by implementing new features or modifying existing Python code based on natural language requests. The tool also integrates testing capabilities to verify the correctness of the generated code. It offers a robust retry mechanism, structured JSON responses, and memory management.

---

## Features
- **Interactive AI Code Assistant**: Accepts user requests in plain language to modify or enhance Python code.
- **Automated Code Generation**: Uses the Llama language model to implement the requested feature.
- **Code Verification**: Runs the generated code snippet and checks it for errors or timeouts.
- **Existing Test Suite Integration**: Optionally runs `pytest` to validate the codebase's stability after modifications.
- **Retry Mechanism**: Attempts multiple retries if the model fails to generate a valid JSON response.
- **Memory Management**: Explicit garbage collection and model unloading to optimize resource usage.

---

## Requirements
- Python 3.8 or higher
- Transformers library: `pip install transformers`
- Pytest (optional for running existing tests): `pip install pytest`
- Huggingface CLI (for model authentication): `pip install huggingface_hub`

---

## Installation
1. Clone this repository:
   ```bash
   git clone https://github.com/your-repo/code-assistant.git
   cd code-assistant
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Authenticate Huggingface account:
   ```bash
   huggingface-cli login
   ```

---

## Usage
Run the script with the target Python file as an argument:
```bash
python assistant.py <source_file.py>
```
The tool will:
1. Prompt you to describe the feature or modification.
2. Generate and propose code changes.
3. Verify the new implementation through existing tests and standalone checks.
4. Allow you to accept or discard the changes.

### Example
```bash
python assistant.py my_script.py
```
**User Input Prompt**:
> Describe the feature you want to implement: Add a function to reverse a string.

---

## Functions and Components

### `assist_user(file_path)`
Manages the user interaction flow, including:
- Loading the target file.
- Collecting the user request.
- Generating and displaying proposed code.
- Running tests to validate correctness.

### `implement_feature(file_content, user_request, num_retries=3)`
Generates modified code based on the user request. Attempts multiple retries if JSON parsing fails.

### `test_code_snippet(code_snippet)`
Executes the provided code snippet in a temporary file and captures errors.

### `test_code_with_existing(file_path)`
Runs `pytest` on the specified file if available.

### `main()`
Initializes the command-line interface and handles argument parsing.

---

## Configuration
- **Model and Tokenizer**: The tool uses `meta-llama/Llama-3.2-1B-Instruct` as the default model. This can be adjusted in the `AutoTokenizer` and `AutoModelForCausalLM` initialization.
- **Timeout Settings**: Code execution timeout is set to 10 seconds for individual snippets and 30 seconds for `pytest`.

---

## Error Handling
- **Timeouts**: Code snippets or tests exceeding the timeout return appropriate error messages.
- **Missing Pytest**: If `pytest` is not installed, a warning is displayed, but the process continues.
- **JSON Parsing Failures**: Retries up to three times to generate valid responses from the language model.

---

## Best Practices
- **Backup Files**: Always maintain a backup of your source files.
- **Limit Complexity**: Start with straightforward requests for better results.
- **Incremental Changes**: Make small, iterative changes to minimize potential issues.

---

## Future Improvements
- Support for more programming languages.
- Integration with version control systems.
- Enhanced error reporting and detailed logging.

---

## License
This project is licensed under the MIT License. See the LICENSE file for more details.
---
