This page consists cheatsheet to use Ollama in different modes via CLI, Python and any other troubleshooting commands.

Note:- This is a soloware cheat sheet for me to use when using ollama. So the content is optimized for my understanding

Operating system:- Ubuntu 24.04.3 LTS <br>
Default ollama service URL - https://localhost:11434 <br>
Ollama python github - https://github.com/ollama/ollama-python/tree/main

**CLI handy commands**
To monitor memory usage and consumption
```
free -g
```
To see top n processes that consume memory (like sorting them by memory consumption)
```
ps aux --sort=-%mem | head -n 4
```
**OLLAMA CLI SPECIFIC**
Installation
```
curl -fsSL https://ollama.com/install.sh | sh
```

Search the available list of models at  https://ollama.com/search

See all the available commands as it relates to ollama
```
ollama
```
You should be able to see something like this (PUT AN IMAGE HERE)

To list all the available environment variables as it relates to ollama
```
ollama serve --all
```
You should be able to see something like this (PUT AN IMAGE HERE)

Pull a model from remote
```
ollama pull <model_name>
```
List available local models
```
ollama list
```
Start ollama service
```
ollama serve
```
This wont automatically run the models you have. It will just start background server with API access. Ideal if you are trying to build an app or expose the model serving via API. 
Plus you get to see all the requests made to the server like burpsuite

Run a specific model
```
ollama run <model_name>
```
Use this to actually start the model instance. This starts an interactive chat session, which is good if you just want chat with the model

Create a customised model using base models
```
ollama create -f <modelfilename>
```
Assuming you already have written your instructions in modelfilename. Reference on how to create a modelfile https://docs.ollama.com/modelfile

Remove a model
```
ollama rm <model_name>
```

List all the models that are running
```
ollama ps
```

Serve ollama models using a different port
```
OLLAMA_HOST = 127.0.0.1:8080 ollama serve
```

To expose ollama service to a local network
```
sudo systemctl edit ollama.service
```
Edit the contents of the said file ny adding
```
[Service]
Environment="OLLAMA_HOST=<YOUR_LOCAL_NETWORK_ADDRESS>"
```
🚨Pay attention to the comments in the service file. Trust me it will save you time. Don't treat this file like bashrc. In bashrc you can append your variables and get over with it but not here 🚨

Restart system daemon
```
sudo systemctl daemon-reload
```
Restart ollama service
```
sudo systemctl restart ollama
```

To stop running a ollama model
```
ollama stop <model_name>
```


API docs – Note that ollama python is built around this itself. So parameters are the same.
https://github.com/ollama/ollama/blob/main/docs/api.md

Killing ollama service - troubleshoot

🚨Ctrl+C wouldnt do the trick most of the times🚨

To stop ollama service
```
sudo systemctl stop ollama.service
```

Killing a running ollama instance on a particular port
```
sudo lsof -i :11434
```

Or figure out the port using
```
ps
```
and kill that process using
```
kill -9 <pid>
```

**Ollama python**
See the notebook above for most commonly used functionalities. Personally saves times instead of reading the documentation, especially the raw api.md
https://github.com/KeerthiNingegowda/ollama_cheatseet/blob/main/ollama_python_api_cheatseet.ipynb



