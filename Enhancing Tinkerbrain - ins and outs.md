> [!abstract] Goal
> - Update the visual component of Tinkerbrain
> 	- Expand+improve the voice notes appearing on the left
> 	- Add outputs
> - Update the data model
> 	- [[#Required updates]]

# Data model

- PersistedMessage
	- `time: ZonedDateTime`
	- `sender: String`
	- `receivers: Set[String]`
	- `participants: Set[String]`
	- `edges: List[TinkerEdge]`
- Graph (sent once)
	- TinkerEdge
		- `source: String`
		- `target: String`
	- TinkerNode
		- `id: String`
		- `color: String`
		- `emoji: Option[String]`
		- `x: Option[Int]`
		- `y: Option[Int]`
		- `href: Option[String]`

## Required updates

- PersistedMessage
	- Add "eventType" e.g.
		- {"input": "voice:base"}
		- {"input": "timer"}
		- {"output": "note:[[Notification Center]]"}
		- {"output": "chime"}
		- {"output": "email"}

# I/O

## Input events

- Voice notes
	- Fast/base 🐢
	- Mid/turbo (new, partial)
	- Slow/large ⚡️
- Timers
- Note updated
- Emails
- (lower priority)
	- Air quality - CO2, AQI
	- Heart rate
	- (future) Pupil dilation

## Outputs

- Note updates
- Smart lights
- Chime
- Smart plugs
- (future) Voice synthesis
