Here is the markdown for the API documentation you provided:

# Server Events

**Beta**  
These are events emitted from the OpenAI Realtime WebSocket server to the client.

---

## error

**Beta**  
Returned when an error occurs.

- `event_id`: `string`  
  The unique ID of the server event.
  
- `type`: `string`  
  The event type, must be `"error"`.
  
- `error`: `object`  
  Details of the error.

### Example

```json
{
  "event_id": "event_890",
  "type": "error",
  "error": {
    "type": "invalid_request_error",
    "code": "invalid_event",
    "message": "The 'type' field is missing.",
    "param": null,
    "event_id": "event_567"
  }
}
```
session.created

Beta
Returned when a session is created. Emitted automatically when a new connection is established.

	•	event_id: string
The unique ID of the server event.
	•	type: string
The event type, must be "session.created".
	•	session: object
The session resource.

Example
```json
{
  "event_id": "event_1234",
  "type": "session.created",
  "session": {
    "id": "sess_001",
    "object": "realtime.session",
    "model": "gpt-4o-realtime-preview-2024-10-01",
    "modalities": ["text", "audio"],
    "instructions": "",
    "voice": "alloy",
    "input_audio_format": "pcm16",
    "output_audio_format": "pcm16",
    "input_audio_transcription": null,
    "turn_detection": {
      "type": "server_vad",
      "threshold": 0.5,
      "prefix_padding_ms": 300,
      "silence_duration_ms": 200
    },
    "tools": [],
    "tool_choice": "auto",
    "temperature": 0.8,
    "max_output_tokens": null
  }
}
```
session.updated

Beta
Returned when a session is updated.

	•	event_id: string
The unique ID of the server event.
	•	type: string
The event type, must be "session.updated".
	•	session: object
The updated session resource.

Example
```json
{
  "event_id": "event_5678",
  "type": "session.updated",
  "session": {
    "id": "sess_001",
    "object": "realtime.session",
    "model": "gpt-4o-realtime-preview-2024-10-01",
    "modalities": ["text"],
    "instructions": "New instructions",
    "voice": "alloy",
    "input_audio_format": "pcm16",
    "output_audio_format": "pcm16",
    "input_audio_transcription": {
      "enabled": true,
      "model": "whisper-1"
    },
    "turn_detection": {
      "type": "none"
    },
    "tools": [],
    "tool_choice": "none",
    "temperature": 0.7,
    "max_output_tokens": 200
  }
}
```
conversation.created

Beta
Returned when a conversation is created. Emitted right after session creation.

	•	event_id: string
The unique ID of the server event.
	•	type: string
The event type, must be "conversation.created".
	•	conversation: object
The conversation resource.

Example
```json
{
  "event_id": "event_9101",
  "type": "conversation.created",
  "conversation": {
    "id": "conv_001",
    "object": "realtime.conversation"
  }
}
```
input_audio_buffer.committed

Beta
Returned when an input audio buffer is committed, either by the client or automatically in server VAD mode.

	•	event_id: string
The unique ID of the server event.
	•	type: string
The event type, must be "input_audio_buffer.committed".
	•	previous_item_id: string
The ID of the preceding item after which the new item will be inserted.
	•	item_id: string
The ID of the user message item that will be created.

Example
```json
{
  "event_id": "event_1121",
  "type": "input_audio_buffer.committed",
  "previous_item_id": "msg_001",
  "item_id": "msg_002"
}
```
input_audio_buffer.cleared

Beta
Returned when the input audio buffer is cleared by the client.

	•	event_id: string
The unique ID of the server event.
	•	type: string
The event type, must be "input_audio_buffer.cleared".

Example
```json
{
  "event_id": "event_1314",
  "type": "input_audio_buffer.cleared"
}
```
input_audio_buffer.speech_started

Beta
Returned in server turn detection mode when speech is detected.

	•	event_id: string
The unique ID of the server event.
	•	type: string
The event type, must be "input_audio_buffer.speech_started".
	•	audio_start_ms: integer
Milliseconds since the session started when speech was detected.
	•	item_id: string
The ID of the user message item that will be created when speech stops.

Example
```json
{
  "event_id": "event_1516",
  "type": "input_audio_buffer.speech_started",
  "audio_start_ms": 1000,
  "item_id": "msg_003"
}
```
input_audio_buffer.speech_stopped

Beta
Returned in server turn detection mode when speech stops.

	•	event_id: string
The unique ID of the server event.
	•	type: string
The event type, must be "input_audio_buffer.speech_stopped".
	•	audio_end_ms: integer
Milliseconds since the session started when speech stopped.
	•	item_id: string
The ID of the user message item that will be created.

Example
```json
{
  "event_id": "event_1718",
  "type": "input_audio_buffer.speech_stopped",
  "audio_end_ms": 2000,
  "item_id": "msg_003"
}
```

conversation.item.created

Beta
Returned when a conversation item is created.

	•	event_id: string
The unique ID of the server event.
	•	type: string
The event type, must be "conversation.item.created".
	•	previous_item_id: string
The ID of the preceding item.
	•	item: object
The item that was created.

Example
```json
{
  "event_id": "event_1920",
  "type": "conversation.item.created",
  "previous_item_id": "msg_002",
  "item": {
    "id": "msg_003",
    "object": "realtime.item",
    "type": "message",
    "status": "completed",
    "role": "user",
    "content": [
      {
        "type": "input_audio",
        "transcript": null
      }
    ]
  }
}
```
conversation.item.input_audio_transcription.completed

Beta
Returned when input audio transcription is enabled and a transcription succeeds.

	•	event_id: string
The unique ID of the server event.
	•	type: string
The event type, must be "conversation.item.input_audio_transcription.completed".
	•	item_id: string
The ID of the user message item.
	•	content_index: integer
The index of the content part containing the audio.
	•	transcript: string
The transcribed text.

Example
```json
{
  "event_id": "event_2122",
  "type": "conversation.item.input_audio_transcription.completed",
  "item_id": "msg_003",
  "content_index": 0,
  "transcript": "Hello, how are you?"
}
```
conversation.item.input_audio_transcription.failed

Beta
Returned when input audio transcription is configured, and a transcription request for a user message failed.

	•	event_id: string
The unique ID of the server event.
	•	type: string
The event type, must be "conversation.item.input_audio_transcription.failed".
	•	item_id: string
The ID of the user message item.
	•	content_index: integer
The index of the content part containing the audio.
	•	error: object
Details of the transcription error.

Example
```json
{
  "event_id": "event_2324",
  "type": "conversation.item.input_audio_transcription.failed",
  "item_id": "msg_003",
  "content"
}
```
