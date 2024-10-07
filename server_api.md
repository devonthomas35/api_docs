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
    "content_index": 0,
    "error": {
        "type": "transcription_error",
        "code": "audio_unintelligible",
        "message": "The audio could not be transcribed.",
        "param": null
    }
}
```

conversation.item.truncated
Beta
Returned when an earlier assistant audio message item is truncated by the client.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "conversation.item.truncated".

item_id
string

The ID of the assistant message item that was truncated.

content_index
integer

The index of the content part that was truncated.

audio_end_ms
integer

The duration up to which the audio was truncated, in milliseconds.

conversation.item.truncated
```json
{
    "event_id": "event_2526",
    "type": "conversation.item.truncated",
    "item_id": "msg_004",
    "content_index": 0,
    "audio_end_ms": 1500
}
```
conversation.item.deleted
Beta
Returned when an item in the conversation is deleted.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "conversation.item.deleted".

item_id
string

The ID of the item that was deleted.

conversation.item.deleted
```json
{
    "event_id": "event_2728",
    "type": "conversation.item.deleted",
    "item_id": "msg_005"
}
```
response.created
Beta
Returned when a new Response is created. The first event of response creation, where the response is in an initial state of "in_progress".

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.created".

response
object

The response resource.


Show properties
response.created
```json
{
    "event_id": "event_2930",
    "type": "response.created",
    "response": {
        "id": "resp_001",
        "object": "realtime.response",
        "status": "in_progress",
        "status_details": null,
        "output": [],
        "usage": null
    }
}
```
response.done
Beta
Returned when a Response is done streaming. Always emitted, no matter the final state.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.done".

response
object

The response resource.


Show properties
response.done
```json
{
    "event_id": "event_3132",
    "type": "response.done",
    "response": {
        "id": "resp_001",
        "object": "realtime.response",
        "status": "completed",
        "status_details": null,
        "output": [
            {
                "id": "msg_006",
                "object": "realtime.item",
                "type": "message",
                "status": "completed",
                "role": "assistant",
                "content": [
                    {
                        "type": "text",
                        "text": "Sure, how can I assist you today?"
                    }
                ]
            }
        ],
        "usage": {
            "total_tokens": 50,
            "input_tokens": 20,
            "output_tokens": 30
        }
    }
}
```
response.output_item.added
Beta
Returned when a new Item is created during response generation.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.output_item.added".

response_id
string

The ID of the response to which the item belongs.

output_index
integer

The index of the output item in the response.

item
object

The item that was added.


Show properties
response.output_item.added
```json
{
    "event_id": "event_3334",
    "type": "response.output_item.added",
    "response_id": "resp_001",
    "output_index": 0,
    "item": {
        "id": "msg_007",
        "object": "realtime.item",
        "type": "message",
        "status": "in_progress",
        "role": "assistant",
        "content": []
    }
}
```json
response.output_item.done
Beta
Returned when an Item is done streaming. Also emitted when a Response is interrupted, incomplete, or cancelled.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.output_item.done".

response_id
string

The ID of the response to which the item belongs.

output_index
integer

The index of the output item in the response.

item
object

The completed item.


Show properties
response.output_item.done
```json
{
    "event_id": "event_3536",
    "type": "response.output_item.done",
    "response_id": "resp_001",
    "output_index": 0,
    "item": {
        "id": "msg_007",
        "object": "realtime.item",
        "type": "message",
        "status": "completed",
        "role": "assistant",
        "content": [
            {
                "type": "text",
                "text": "Sure, I can help with that."
            }
        ]
    }
}
```
response.content_part.added
Beta
Returned when a new content part is added to an assistant message item during response generation.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.content_part.added".

response_id
string

The ID of the response.

item_id
string

The ID of the item to which the content part was added.

output_index
integer

The index of the output item in the response.

content_index
integer

The index of the content part in the item's content array.

part
object

The content part that was added.


Show properties
response.content_part.added
```json
{
    "event_id": "event_3738",
    "type": "response.content_part.added",
    "response_id": "resp_001",
    "item_id": "msg_007",
    "output_index": 0,
    "content_index": 0,
    "part": {
        "type": "text",
        "text": ""
    }
}
```
response.content_part.done
Beta
Returned when a content part is done streaming in an assistant message item. Also emitted when a Response is interrupted, incomplete, or cancelled.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.content_part.done".

response_id
string

The ID of the response.

item_id
string

The ID of the item.

output_index
integer

The index of the output item in the response.

content_index
integer

The index of the content part in the item's content array.

part
object

The content part that is done.


Show properties
response.content_part.done
```json
{
    "event_id": "event_3940",
    "type": "response.content_part.done",
    "response_id": "resp_001",
    "item_id": "msg_007",
    "output_index": 0,
    "content_index": 0,
    "part": {
        "type": "text",
        "text": "Sure, I can help with that."
    }
}
```
response.text.delta
Beta
Returned when the text value of a "text" content part is updated.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.text.delta".

response_id
string

The ID of the response.

item_id
string

The ID of the item.

output_index
integer

The index of the output item in the response.

content_index
integer

The index of the content part in the item's content array.

delta
string

The text delta.

response.text.delta
```json
{
    "event_id": "event_4142",
    "type": "response.text.delta",
    "response_id": "resp_001",
    "item_id": "msg_007",
    "output_index": 0,
    "content_index": 0,
    "delta": "Sure, I can h"
}
```
response.text.done
Beta
Returned when the text value of a "text" content part is done streaming. Also emitted when a Response is interrupted, incomplete, or cancelled.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.text.done".

response_id
string

The ID of the response.

item_id
string

The ID of the item.

output_index
integer

The index of the output item in the response.

content_index
integer

The index of the content part in the item's content array.

text
string

The final text content.

response.text.done
```json
{
    "event_id": "event_4344",
    "type": "response.text.done",
    "response_id": "resp_001",
    "item_id": "msg_007",
    "output_index": 0,
    "content_index": 0,
    "text": "Sure, I can help with that."
}
```
response.audio_transcript.delta
Beta
Returned when the model-generated transcription of audio output is updated.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.audio_transcript.delta".

response_id
string

The ID of the response.

item_id
string

The ID of the item.

output_index
integer

The index of the output item in the response.

content_index
integer

The index of the content part in the item's content array.

delta
string

The transcript delta.

response.audio_transcript.delta
```json
{
    "event_id": "event_4546",
    "type": "response.audio_transcript.delta",
    "response_id": "resp_001",
    "item_id": "msg_008",
    "output_index": 0,
    "content_index": 0,
    "delta": "Hello, how can I a"
}
```
response.audio_transcript.done
Beta
Returned when the model-generated transcription of audio output is done streaming. Also emitted when a Response is interrupted, incomplete, or cancelled.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.audio_transcript.done".

response_id
string

The ID of the response.

item_id
string

The ID of the item.

output_index
integer

The index of the output item in the response.

content_index
integer

The index of the content part in the item's content array.

transcript
string

The final transcript of the audio.

response.audio_transcript.done
```json
{
    "event_id": "event_4748",
    "type": "response.audio_transcript.done",
    "response_id": "resp_001",
    "item_id": "msg_008",
    "output_index": 0,
    "content_index": 0,
    "transcript": "Hello, how can I assist you today?"
}
```
response.audio.delta
Beta
Returned when the model-generated audio is updated.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.audio.delta".

response_id
string

The ID of the response.

item_id
string

The ID of the item.

output_index
integer

The index of the output item in the response.

content_index
integer

The index of the content part in the item's content array.

delta
string

Base64-encoded audio data delta.

response.audio.delta
```json
{
    "event_id": "event_4950",
    "type": "response.audio.delta",
    "response_id": "resp_001",
    "item_id": "msg_008",
    "output_index": 0,
    "content_index": 0,
    "delta": "Base64EncodedAudioDelta"
}
```
response.audio.done
Beta
Returned when the model-generated audio is done. Also emitted when a Response is interrupted, incomplete, or cancelled.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.audio.done".

response_id
string

The ID of the response.

item_id
string

The ID of the item.

output_index
integer

The index of the output item in the response.

content_index
integer

The index of the content part in the item's content array.

response.audio.done
```json
{
    "event_id": "event_5152",
    "type": "response.audio.done",
    "response_id": "resp_001",
    "item_id": "msg_008",
    "output_index": 0,
    "content_index": 0
}
```
response.function_call_arguments.delta
Beta
Returned when the model-generated function call arguments are updated.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.function_call_arguments.delta".

response_id
string

The ID of the response.

item_id
string

The ID of the function call item.

output_index
integer

The index of the output item in the response.

call_id
string

The ID of the function call.

delta
string

The arguments delta as a JSON string.

response.function_call_arguments.delta
```json
{
    "event_id": "event_5354",
    "type": "response.function_call_arguments.delta",
    "response_id": "resp_002",
    "item_id": "fc_001",
    "output_index": 0,
    "call_id": "call_001",
    "delta": "{\"location\": \"San\""
}
```
response.function_call_arguments.done
Beta
Returned when the model-generated function call arguments are done streaming. Also emitted when a Response is interrupted, incomplete, or cancelled.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "response.function_call_arguments.done".

response_id
string

The ID of the response.

item_id
string

The ID of the function call item.

output_index
integer

The index of the output item in the response.

call_id
string

The ID of the function call.

arguments
string

The final arguments as a JSON string.

response.function_call_arguments.done
```json
{
    "event_id": "event_5556",
    "type": "response.function_call_arguments.done",
    "response_id": "resp_002",
    "item_id": "fc_001",
    "output_index": 0,
    "call_id": "call_001",
    "arguments": "{\"location\": \"San Francisco\"}"
}
```
rate_limits.updated
Beta
Emitted after every "response.done" event to indicate the updated rate limits.

event_id
string

The unique ID of the server event.

type
string

The event type, must be "rate_limits.updated".

rate_limits
array

List of rate limit information.


Show properties
rate_limits.updated
```json
{
    "event_id": "event_5758",
    "type": "rate_limits.updated",
    "rate_limits": [
        {
            "name": "requests",
            "limit": 1000,
            "remaining": 999,
            "reset_seconds": 60
        },
        {
            "name": "tokens",
            "limit": 50000,
            "remaining": 49950,
            "reset_seconds": 60
        }
    ]
}
```
