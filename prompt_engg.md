# Prompt engineering Techniques
- COT Chain of thoughts, instead of a single prompt ask to think in a stepwise fashion. May add some examples
- Self consistency: Ask multiple expert opinion and choose the one with consistency in the answers.
- Tree of thoughts for more open eneded promblem solving. Insted of one liner chain of though can brnach out and backtrack
- REACT: reason and act, like LLM calling tools, running code and checking answer and prepare for next step
# Best practices
- use exampels, one shot few shots
- Use string action verb, tell model exactly what to do
- use instructions over constraints. Dont use these libraries vs use these libraries
# Agent
- Google Agent builder engine
- Vertex AI Eval service. Integrates with monitoring etc.
  # Agentic Rag
   agent actively refines queries(like how to pair my phone in car manual agentic ai), parse user query 
  , evaluate search results into multiple steps
   and search for the best possible match then finally combine, even refine further.

  All this depends on the search being finely tuned. Better chunking and adding context(tag, synonyms etc.) into chunk
  Also better vector database, rankers, check grounding(fact checking, ai can provide the reference for fact).

  Finally they need to be transparent, accountable, robust and fair
 ## Google cloud tools
  Vertex AI search, Vertex AI search builder AI, Vertex AI Rag Engine
   # Agent as contractors
  - AI Contract concept
  ?? Outline exactly what one, need, penalties. Making it accountable.
