# BlindMLClient

**BlindMLClient** is a Python client library designed to interact with the [BlindMLServer](https://github.com/blindml-ai/blindml-server), which hosts models powered by Fully Homomorphic Encryption (FHE).   
It enables users to perform secure, encrypted predictions without ever exposing raw input data — ensuring full privacy throughout the inference pipeline.



## ✨ Features

- Initialize a secure connection with an FHE-enabled inference server
- Encrypt input data using Fully Homomorphic Encryption (FHE)
- Send encrypted data and perform remote inference
- Decrypt the server's encrypted prediction result into readable output
- Supports integration with [Concrete-ML](https://docs.zama.ai/concrete-ml/)



## 📦Installation

This project uses [Zama's Concrete-ML](https://github.com/zama-ai/concrete-ml) library.  
For the best compatibility and performance, it is **highly recommended to run it within a Conda environment**.

### Prerequisites

Please make sure you have [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or [Anaconda](https://www.anaconda.com/) installed.

### Create Conda Environment and Install Packages

Run the following commands in your terminal to set up the environment:

```bash
# 1. Create a Conda environment named 'concrete-env' with Python 3.8
conda create -n blindml-env python=3.8 -y

# 2. Activate the environment
conda activate blindml-env

# 3. (Optional) Upgrade pip
python -m pip install --upgrade pip

# 4. Install concrete-ml version 1.4.0
pip install concrete-ml==1.4.0
```
Then install blindml
```bash
pip install blindml
```

## 🚀 Example Usage
```python
import blindml

# Define server URL and your API key
SERVER_URL = "http://127.0.0.1:3000/proxy/cm/43f75fc1-488e-4ebb-82dd-2f59ee80f3ce"
API_KEY = "YOUR_API_KEY"

# Initialize the client
bm = blindml()
bm.init(server_url=SERVER_URL, api_key=API_KEY)

# Example input (e.g., model features)
input_data = [1.5, 2.3, 3.7]

# Step 1: Encrypt the input
encrypted_input = bm.encrypt(input_data)

# Step 2: Send encrypted input and receive encrypted prediction
encrypted_prediction = bm.predict(encrypted_input)

# Step 3: Decrypt the result
prediction = bm.decrypt(encrypted_prediction)

print("Prediction result:", prediction)
```

## 📚 API Methods

### `init(server_url: str, api_key: str) -> None`
Initializes the BlindMLClient with the server’s endpoint and your authentication key.

- **Parameters**:  
  - `server_url`: URL of the deployed BlindMLServer  
  - `api_key`: API key used for authenticating the client

---

### `encrypt(input_data: Any) -> EncryptedData`
Encrypts the input data using Fully Homomorphic Encryption (FHE).  
This prepares the input for secure inference.

- **Parameters**:  
  - `input_data`: Input data formatted according to the model's expected input schema  
    *(e.g., a list of floats, dictionary, or other structure depending on the model)*

- **Returns**:  
  - Encrypted version of the input data

---

### `predict(encrypted_input: EncryptedData) -> EncryptedResult`
Sends the encrypted input to the server and receives an encrypted prediction result.

- **Parameters**:  
  - `encrypted_input`: The output from the `encrypt()` method

- **Returns**:  
  - An encrypted prediction result returned by the server

---

### `decrypt(encrypted_result: EncryptedResult) -> Any`
Decrypts the server’s encrypted prediction and returns it in a human-readable format.

- **Parameters**:  
  - `encrypted_result`: The encrypted result from the `predict()` method

- **Returns**:  
  - The final decrypted prediction (e.g., a float or label)


## 📌 Notes
This client library must be used with a running instance of [BlindMLServer](https://github.com/blindml-ai/blindml-server)

All communication and computation are based on Fully Homomorphic Encryption (FHE), providing end-to-end data privacy














