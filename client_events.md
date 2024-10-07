# Client Events (Beta)

These are events that the OpenAI Realtime WebSocket server will accept from the client.

Learn more about the Realtime API.

---

## `session.update` (Beta)

Send this event to update the session’s default configuration.

### Properties:

- `event_id`: `string` (optional)  
  Optional client-generated ID used to identify this event.

- `type`: `string`  
  The event type, must be `"session.update"`.

- `session`: `object`  
  Session configuration to update.

#### Example:

```json
{
    "event_id": "event_123",
    "type": "session.update",
    "session": {
        "modalities": ["text", "audio"],
        "instructions": "Your knowledge cutoff is 2023-10. You are a helpful assistant.",
        "voice": "alloy",
        "input_audio_format": "pcm16",
        "output_audio_format": "pcm16",
        "input_audio_transcription": {
            "enabled": true,
            "model": "whisper-1"
        },
        "turn_detection": {
            "type": "server_vad",
            "threshold": 0.5,
            "prefix_padding_ms": 300,
            "silence_duration_ms": 200
        },
        "tools": [
            {
                "type": "function",
                "name": "get_weather",
                "description": "Get the current weather for a location.",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "location": { "type": "string" }
                    },
                    "required": ["location"]
                }
            }
        ],
        "tool_choice": "auto",
        "temperature": 0.8,
        "max_output_tokens": null
    }
}
```
input_audio_buffer.append (Beta)

Send this event to append audio bytes to the input audio buffer.

Properties:

	•	event_id: string (optional)
Optional client-generated ID used to identify this event.
	•	type: string
The event type, must be "input_audio_buffer.append".
	•	audio: string
Base64-encoded audio bytes.

Example:

{
    "event_id": "event_456",
    "type": "input_audio_buffer.append",
    "audio": "Base64EncodedAudioData"
}

input_audio_buffer.commit (Beta)

Send this event to commit audio bytes to a user message.

Properties:

	•	event_id: string (optional)
Optional client-generated ID used to identify this event.
	•	type: string
The event type, must be "input_audio_buffer.commit".

Example:

{
    "event_id": "event_789",
    "type": "input_audio_buffer.commit"
}

input_audio_buffer.clear (Beta)

Send this event to clear the audio bytes in the buffer.

Properties:

	•	event_id: string (optional)
Optional client-generated ID used to identify this event.
	•	type: string
The event type, must be "input_audio_buffer.clear".

Example:

{
    "event_id": "event_012",
    "type": "input_audio_buffer.clear"
}

conversation.item.create (Beta)

Send this event when adding an item to the conversation.

Properties:

	•	event_id: string (optional)
Optional client-generated ID used to identify this event.
	•	type: string
The event type, must be "conversation.item.create".
	•	previous_item_id: string
The ID of the preceding item after which the new item will be inserted.
	•	item: object
The item to add to the conversation.

Example:

{
    "event_id": "event_345",
    "type": "conversation.item.create",
    "previous_item_id": null,
    "item": {
        "id": "msg_001",
        "type": "message",
        "status": "completed",
        "role": "user",
        "content": [
            {
                "type": "input_text",
                "text": "Hello, how are you?"
            }
        ]
    }
}

conversation.item.truncate (Beta)

Send this event when you want to truncate a previous assistant message’s audio.

Properties:

	•	event_id: string (optional)
Optional client-generated ID used to identify this event.
	•	type: string
The event type, must be "conversation.item.truncate".
	•	item_id: string
The ID of the assistant message item to truncate.
	•	content_index: integer
The index of the content part to truncate.
	•	audio_end_ms: integer
Inclusive duration up to which audio is truncated, in milliseconds.

Example:

{
    "event_id": "event_678",
    "type": "conversation.item.truncate",
    "item_id": "msg_002",
    "content_index": 0,
    "audio_end_ms": 1500
}

conversation.item.delete (Beta)

Send this event when you want to remove any item from the conversation history.

Properties:

	•	event_id: string (optional)
Optional client-generated ID used to identify this event.
	•	type: string
The event type, must be "conversation.item.delete".
	•	item_id: string
The ID of the item to delete.

Example:

{
    "event_id": "event_901",
    "type": "conversation.item.delete",
    "item_id": "msg_003"
}

response.create (Beta)

Send this event to trigger a response generation.

Properties:

	•	event_id: string (optional)
Optional client-generated ID used to identify this event.
	•	type: string
The event type, must be "response.create".
	•	response: object
Configuration for the response.

Example:

{
    "event_id": "event_234",
    "type": "response.create",
    "response": {
        "modalities": ["text", "audio"],
        "instructions": "Please assist the user.",
        "voice": "alloy",
        "output_audio_format": "pcm16",
        "tools": [
            {
                "type": "function",
                "name": "calculate_sum",
                "description": "Calculates the sum of two numbers.",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "a": { "type": "number" },
                        "b": { "type": "number" }
                    },
                    "required": ["a", "b"]
                }
            }
        ],
        "tool_choice": "auto",
        "temperature": 0.7,
        "max_output_tokens": 150
    }
}

response.cancel (Beta)

Send this event to cancel an in-progress response.

Properties:

	•	event_id: string (optional)
Optional client-generated ID used to identify this event.
	•	type: string
The event type, must be "response.cancel".
