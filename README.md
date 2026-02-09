<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>

<body>
  <div class="container">
<!-- TITLE -->

  <h1>Structured Output Design Patterns for Large Language Models</h1>
  
  <h3> TypedDict & Pydantic Output Parsers with LangChain
  </h3>

  
<div
    <!-- INTRO -->
    <p>
      This repository documents practical and production-ready techniques
      for generating <strong>reliable structured outputs</strong> from
      Large Language Models (LLMs), with a focus on
      <strong>open-source models</strong>.
    </p>
<div
    <p>
      It explains how to design data formats, when native structured output
      works, and when output parsers are required.
    </p>
<div
    <hr />
<div
    <!-- WHY IT MATTERS -->
    <h2>Why Structured Output Matters</h2>
<div
    <p>
      LLMs are probabilistic text generators. Without strict enforcement,
      outputs can vary across invocations.
    </p>
<div
    <ul>
      <li>Missing or renamed fields</li>
      <li>Incorrect data types</li>
      <li>Malformed JSON</li>
      <li>Silent downstream failures</li>
    </ul>

  <pre>

  {
  "name": "Shrutika",
  "experience": 2,
  "skills": ["Python", "Machine Learning"]
  }

</pre>
<div
    <p>
      Structured output ensures responses are predictable and safe for
      programmatic use.
    </p>
<div
    <hr />
<div
    <!-- DATA FORMAT -->
    <h2>Data Format as a Contract</h2>
<div
    <p>
      A <strong>Data Format</strong> defines a contract between:
    </p>
<div
    <ul>
      <li>The LLM</li>
      <li>Your application logic</li>
      <li>Downstream systems (APIs, agents, databases)</li>
    </ul>
<div
    <p>
      This contract specifies required fields, data types, and output shape
      before generation occurs.
    </p>
<div
    <hr />
<div
    <!-- NATIVE STRUCTURED OUTPUT -->
    <h2>Approach 1: Native Structured Output</h2>
<div
    <p>
      Some models allow attaching a schema directly before invocation.
    </p>

<pre>
structured_model = model.with_structured_output(DataFormat)
response = structured_model.invoke(prompt)
</pre>
<div
    <div class="warning">
      Most open-source LLMs do not reliably support native structured output.
      Use this approach only when model behavior is well validated.
    </div>
<div
    <hr />
<div
    <!-- OUTPUT PARSERS -->
    <h2>Approach 2: Output Parsers (Recommended)</h2>
<div
    <p>
      Output parsers convert unstructured LLM text into structured,
      schema-compliant data.
    </p>
<div
    <!-- TYPEDDICT -->
    <h3>TypedDict: Lightweight Schema</h3>
  
  <pre>
    
  class DataFormat(TypedDict):
    summary: str
    experience: Optional[int]
    skills: list[str]
    links: list[str]
  </pre>
  
  <ul>
      <li>Defines expected structure only</li>
      <li>No runtime validation</li>
      <li>Best for experimentation</li>
    </ul>
 <div 
    <!-- PYDANTIC -->
    <h3>Pydantic Output Parser: Strict Validation</h3>

  <pre>
class DataFormat(BaseModel):
    summary: str
    experience: Optional[int]
    skills: list[str]
    </pre>
<div
    <ul>
      <li>Strict schema enforcement</li>
      <li>Type-safe parsing</li>
      <li>Production-ready</li>
    </ul>
<div
    <div class="callout">
      <strong>Design Principle:</strong>
      If an LLM output is consumed by code, it must be validated.
    </div>

  <hr />
<div
    <!-- FLOW -->
    <h2>Structured Output Flow</h2>
<div
    <p>
      The flow below illustrates how structured output is generated based
      on model capabilities and parser choice.
    </p>
<div
    <div class="flowchart">
      <strong>Structured Output Code Execution Flow with LangChain</strong><br /><br />
        <img width="745" height="577" alt="Screenshot 2026-02-09 103306" src="https://github.com/user-attachments/assets/f5aafd13-bc3a-44ae-8fcd-a007519741fc" />

</div>

 

  

   
  </div>
</body>
</html>
