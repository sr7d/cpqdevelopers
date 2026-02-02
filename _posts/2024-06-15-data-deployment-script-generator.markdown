---
layout: post
title: Data Deployment Script Generator
description: This tool allows you to create a reusable data deployment script using anonymous apex. Follow these steps to create your script.
date: 2024-06-15 10:00:00 +0300
author: admin
image: /images/scriptGenerator.png
hide_image: true
image_caption:
tags: [tools, legacy-cpq, revenue-cloud]
featured:
video_embed:
permalink: /data-deployment-script-generator/
---
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/styles/atom-one-dark.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/highlight.min.js"></script>

<style>
  .generator-steps {
    background: var(--secondary-color, #F6F9FC);
    border-radius: 12px;
    padding: 24px;
    margin-bottom: 24px;
  }
  .generator-steps ol {
    margin: 0;
    padding-left: 24px;
  }
  .generator-steps li {
    padding: 8px 0;
    line-height: 1.6;
  }
  .generator-steps a {
    color: var(--primary-color, #A82D5B);
    text-decoration: none;
    border-bottom: 1px solid transparent;
    transition: border-color 0.2s;
  }
  .generator-steps a:hover {
    border-bottom-color: var(--primary-color, #A82D5B);
  }
  .input-container {
    margin-bottom: 16px;
  }
  #jsonInput {
    width: 100%;
    height: 280px;
    padding: 16px;
    border: 2px solid var(--border-color, #eee);
    border-radius: 12px;
    font-size: 14px;
    font-family: 'SF Mono', 'Monaco', 'Inconsolata', 'Fira Code', monospace;
    background: var(--white, #fff);
    transition: border-color 0.2s, box-shadow 0.2s;
    resize: vertical;
  }
  #jsonInput:focus {
    outline: none;
    border-color: var(--primary-color, #A82D5B);
    box-shadow: 0 0 0 3px rgba(168, 45, 91, 0.1);
  }
  .button-row {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-top: 16px;
  }
  #copied {
    color: #03b800;
    font-weight: 600;
  }
  #outputContainer {
    margin-top: 24px;
  }
  #outputText {
    background: #282c34;
    color: #abb2bf;
    border-radius: 12px;
    padding: 20px;
    font-size: 13px;
    line-height: 1.5;
    overflow-x: auto;
    max-height: 500px;
  }
</style>
<div class="input-container">
  <textarea id="jsonInput" placeholder="Query data from Salesforce using Salesforce Inspector. Copy and paste it here."></textarea>
</div>

<div class="button-row">
  <button class="button button--primary" onclick="generateScript()">Generate Apex</button>
  <button class="button button--primary" onclick="copyToClipboard()" style="display: none;">Copy to Clipboard</button>
  <span id="copied" style="display: none;">Copied!</span>
  <br>
</div>

<div id="outputContainer" style="display: none;">
  <pre id="outputText" class="language-apex"></pre>
</div>

<script>
  function generateScript() {
    const jsonInput = document.getElementById('jsonInput').value;
    let jsonData;

    try {
      jsonData = JSON.parse(jsonInput);
    } catch (error) {
      alert('Invalid JSON data');
      return;
    }

    const objectType = jsonData[0]?.attributes?.type || "UnknownType";
    let script = `Map<String, Map<String, Object>> objectSettings = new Map<String, Map<String, Object>>{\n`;

    jsonData.forEach((item, index) => {
      let Name = item.Name ? item.Name.replace(/'/g, "\\'") : `Object_${index}`;
      script += `'${Name}' => new Map<String, Object>{\n`;
      script += `'targetObject' => new ${objectType}(\n`;

      for (let key in item) {
        if (key !== "attributes") {
          let value = item[key];
          let formattedValue;

          if (typeof value === 'boolean' || value === null) {
            formattedValue = value;
          } else if (typeof value === 'number') {
            formattedValue = value;
          } else {
            formattedValue = `'${value.replace(/'/g, "\\'")}'`;
          }

          script += `${key}=${formattedValue},\n`;
        }
      }

      script = script.slice(0, -2) + '\n';
      script += ")\n},\n";
    });

    script = script.slice(0, -2) + '\n};\n';

    script += `for (String Name : objectSettings.keySet()) {
      Map<String, Object> settings = objectSettings.get(Name);
      ${objectType} targetObject = (${objectType}) settings.get('targetObject');
      List<${objectType}> existingObject = [
        SELECT Id
        FROM ${objectType}
        WHERE Id = :targetObject.Id
        ORDER BY CreatedDate DESC
      ];
      if (!existingObject.isEmpty()) {
        targetObject.Id = existingObject[0].Id;
      }
      upsert targetObject;
    }`;

    document.getElementById('jsonInput').style.display = 'none';
    document.querySelector('button[onclick="generateScript()"]').style.display = 'none';
    document.querySelector('button[onclick="copyToClipboard()"]').style.display = '';
    document.getElementById('outputContainer').style.display = 'block';

    // Set output text and highlight the code
    document.getElementById('outputText').textContent = script;
    hljs.highlightElement(document.getElementById('outputText'));
  }

  function copyToClipboard() {
    const outputText = document.getElementById('outputText').textContent;
    const tempTextArea = document.createElement('textarea');
    tempTextArea.value = outputText;
    document.body.appendChild(tempTextArea);
    tempTextArea.select();
    document.execCommand('copy');
    document.body.removeChild(tempTextArea);
    document.getElementById('copied').style.display = '';
  }
</script>
