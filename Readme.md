**The Problem:** Voice agents often lack "memory" or access to specific proprietary data, resulting in generic responses.

**The Solution:** A high-speed Retrieval-Augmented Generation (RAG) pipeline that allows an ElevenLabs voice agent to "query" a private knowledge base in real-time.

**Technical Highlights:**

Vector Search: Queries a Supabase (PostgreSQL) vector database using pgvector to find relevant document chunks based on the user's spoken input.

Webhook Architecture: Handles the low-latency handshake between ElevenLabs' conversational interface and the n8n logic engine.

Knowledge Retrieval: Efficiently pipes the most relevant text data back to the voice model to ensure high-accuracy responses during live calls.