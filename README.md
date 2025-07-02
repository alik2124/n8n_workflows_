
# WhatsApp Media AI Processing Workflow

This repository contains an n8n automation workflow that processes incoming WhatsApp messages using AI. The workflow handles audio, image, and text-based messages and responds with AI-generated replies either as text or audio.



## Features

* Audio Processing

  * Downloads WhatsApp audio.
  * Transcribes it into text using OpenAI Whisper or an external transcription API.
  * Sends the transcribed text to an AI agent for response generation.

* Image Processing

  * Downloads images from WhatsApp.
  * Analyzes the image using AI for captioning, analysis, or description.
  * Sends the result to an AI agent to generate a reply.

* Text Processing

  * Directly sends text messages to the AI agent for response generation.

* AI Responses

  * AI-generated replies are sent as text or optionally converted into audio.

* Multi-format Reply

  * Based on logic, the bot can send either text or audio replies back to WhatsApp.


## Workflow Explanation

### 1. Trigger - WhatsApp Trigger

Starts the workflow when a message (text, image, or audio) is received on WhatsApp.

### 2. Switch Node - Message Type Detection

Routes the workflow based on the type of message:

* Text
* Audio
* Image


### For Audio Messages

* Download Media: Downloads the audio file from WhatsApp.
* HTTP Request: Sends the audio file to an external transcription service.
* Transcribe a Recording: Converts speech to text using OpenAI Whisper or other APIs.
* Edit Fields: Cleans or transforms the transcribed text for the AI agent.


### For Image Messages

* Download Media: Downloads the image file from WhatsApp.
* HTTP Request: Sends the image to an external image analysis API.
* Analyze Image: AI interprets or captions the image.
* Edit Fields: Formats the AI result for the AI agent.


### For Text Messages

* Passes directly from the Switch Node to the Edit Fields node, preparing the message for the AI agent.


### AI Agent

This is the core of the workflow. It uses an OpenAI GPT model (or any other LLM) to:

* Interpret the input (text, transcription, or image analysis).
* Generate a human-like response.

Note: The memory node is deactivated but can be enabled to maintain chat context.


### IF Node - Response Type Decision

Determines if the AI's response should be sent as text or audio.

* If audio is needed:

  * Generate Audio: Converts the AI-generated text into speech.
* If text is sufficient:

  * Proceeds directly to send as text.


### Code Node (Optional)

Applies additional formatting, post-processing, or custom logic to the AI-generated response.


### Send Message Nodes

Sends the final response back to the WhatsApp user either as:

* Text message
* Audio message


## Dependencies

* n8n (self-hosted or cloud)
* WhatsApp API (via Meta or another provider)
* OpenAI (GPT for language tasks and Whisper for speech-to-text)
* Optional: Image analysis APIs (Google Vision, AWS Rekognition, etc.)
* Optional: Text-to-Speech service (Google TTS, ElevenLabs, etc.)


## Deployment Steps

1. Clone this repository.
2. Import the workflow JSON into your n8n instance.
3. Configure credentials for:

   * WhatsApp
   * OpenAI or any AI service
   * Optional APIs (image analysis, TTS, etc.)
4. Activate the workflow in n8n.


## Notes

* The memory node is disabled by default but can be enabled for maintaining conversation history.
* This workflow is modular and handles different media types individually with their own processing paths.



## Contribution

Contributions are welcome. Feel free to fork the repository, submit issues, and open pull requests.



## License

This project is licensed under the MIT License.


If you would like, I can format this into a downloadable `README.md` file for you. Would you like that?
