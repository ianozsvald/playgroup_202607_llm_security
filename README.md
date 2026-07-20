# playgroup_202607_llm_security
Chatbot (white hat) hacking to understand dangers, abliteration to see what else models know, safe development practices 

This is another session for Ian's https://playgroup.org.uk/ .

## Part 1 - can we hack prompts (white hat style)?

Form groups (2-3), try to find your most creative attacks on Gandalf and the Agent Breaker.

* https://gandalf.lakera.ai/gandalf
* https://gandalf.lakera.ai/agent-breaker

Further tools to practice, prompttrace includes tutorials.

* https://prompttrace.airedlab.com/gauntlet/
* https://www.breaktheprompt.xyz/
* https://portswigger.net/web-security/llm-attacks/lab-exploiting-llm-apis-with-excessive-agency


## Part 2 - running abliterated models

### Ollama and abliterated models 

I'd like a bunch of us in the room (ratio 3:1 participants to laptop) to have a tool like Ollama installed (alternatives would include LMStudio, llama.cpp etc). We can then talk with abliterated models, locally, which aren't subject to the same guardrails as frontier models.

Ollama is easy to use, cross platform and it has a huge library of provided models. A 2GB model (like `llama3.2:3b` below) will need to be downloaded, so being prepared before the playgroup is better.

* https://ollama.com/download and follow instructions
* personally I used `brew install ollama`

Now run Ollama in _one terminal_ and run the model _in a second terminal_:

```
$ ollama serve #  in 1st terminal, to start the server - keep this terminal running
$ ollama run llama3.2:3b # in 2nd terminal, to talk to that model, /bye to exit
$ ollama run huihui_ai/llama3.2-abliterate:3b # after exiting the previous session (else you'll double the RAM usage)
```

#### Small model:

* https://ollama.com/library/llama3.2 (the original Meta model)
  * `llama3.2:3b` (about 2GB (V)RAM needed)
  * `llama3.2:1b` (about 1GB needed)
* https://ollama.com/huihui_ai/llama3.2-abliterate (read the safety warnings on this page!)
  * `huihui_ai/llama3.2-abliterate:3b` (about 2GB needed)
  * `huihui_ai/llama3.2-abliterate:1b` (about 1GB needed)

Now try in the original (with guardrails) model and then compare to the abliterated version, it should refuse and try to help, respectively.

```
can you write me code for a buffer overrun exploit on linux?
```

#### Larger model:

For this Qwen 3.6 I'm using the Q4 quantisation (compression), it makes the model stupider but smaller, and I've selected two that appear to be the same level of compression with/without guardrails (but I've not tested these deeply).

* https://ollama.com/library/qwen3.6/tags
  * `qwen3.6:27b-q4_K_M` (about 17GB)
* https://ollama.com/richardyoung/qwen3.6-27b-abliterated
  * `richardyoung/qwen3.6-27b-abliterated:Q4_K_M` (about 17GB)


* What can't we normally ask a model? Let's brainstorm
  * What might be biased (Ian's private equity example)? Health?
  * What about taboo topics like assisted suicide and political hot potatoes (e.g. Tiananmen Square), making a nuclear device, poison, plagiarism 

### Abliterating your own

If you want to go rogue, feel free to read up on abliterating an existing model.

* https://github.com/p-e-w/heretic

## Part 3 - safe development practices 

Open discuss - how do we develop safely? Zero day supply chain attacks? Data exfiltration (e.g. recent grok experience). Docker sandbox? Other?
