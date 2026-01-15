# Working with Docker Labels
## Overview
Docker labels are a way to add custom metadata to your images, helping you organize them by project, record licensing information, aid in automation, or for other reasons. This guide will walk you through the process of adding labels to your Docker images, including the syntax, usage examples, and how to view an image's labels.

## Prerequisites
No specific prerequisites are mentioned in the provided lab content. However, it is assumed that you have a basic understanding of Docker and its commands.

## Step-by-Step Instructions
To add labels to your Docker image, follow these steps:
1. Open your Dockerfile and add a line starting with `LABEL`.
2. Specify one or more key-value pairs after the `LABEL` instruction.
3. Use quotes and backslashes to include spaces within a label value, as you would in command-line parsing.
4. You can specify multiple labels on a single line, separated by spaces.
5. To view an image's labels, use the `docker inspect` command.

### Label Syntax
The label syntax in your Dockerfile is as follows:
```bash
LABEL <key>=<value> <key>=<value> <key>=<value> ...
```
### Usage Examples
Here are a few examples of how to use the `LABEL` instruction:
```bash
LABEL "com.example.vendor"="ACME Incorporated"
LABEL com.example.label-with-value="foo"
LABEL version="1.0"
LABEL description="This text illustrates \
that label-values can span multiple lines."
```
You can also specify multiple labels on a single line:
```bash
LABEL multi.label1="value1" multi.label2="value2" other="value3"
```
Or, you can use backslashes to span multiple lines:
```bash
LABEL multi.label1="value1" \
multi.label2="value2" \
other="value3"
```

## Expected Output
When you use the `docker inspect` command to view an image's labels, you should see a JSON object with a "Labels" section:
```json
"Labels": {
  "com.example.vendor": "ACME Incorporated",
  "com.example.label-with-value": "foo",
  "version": "1.0",
  "description": "This text illustrates that label-values can span multiple lines.",
  "multi.label1": "value1",
  "multi.label2": "value2",
  "other": "value3"
},
```

## Key Concepts
* Docker labels are key-value pairs that add custom metadata to your images.
* Labels can be used to organize images, record licensing information, aid in automation, or for other reasons.
* The `LABEL` instruction is used to add metadata to an image.
* Labels can be specified on a single line, separated by spaces, or span multiple lines using backslashes.
* The `docker inspect` command is used to view an image's labels.
* Labels included in base or parent images are inherited by your image, and the most-recently-applied value overrides any previously-set value.

By following these steps and understanding the concepts outlined above, you should be able to effectively use Docker labels to add custom metadata to your images.

---

