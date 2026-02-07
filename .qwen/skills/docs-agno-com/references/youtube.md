# Youtube

**Source:** https://docs.agno.com/tools/toolkits/others/youtube.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Youtube

**YouTubeTools** enable an Agent to access captions and metadata of YouTube videos, when provided with a video URL.

## Prerequisites

The following example requires the `youtube_transcript_api` library.

```shell  theme={null}
uv pip install -U youtube_transcript_api
```

## Example

The following agent will provide a summary of a YouTube video.

```python cookbook/14_tools/youtube_tools.py theme={null}
from agno.agent import Agent
from agno.tools.youtube import YouTubeTools

agent = Agent(
    tools=[YouTubeTools()],
        description="You are a YouTube agent. Obtain the captions of a YouTube video and answer questions.",
)

agent.print_response("Summarize this video https://www.youtube.com/watch?v=Iv9dewmcFbs&t", markdown=True)
```

## Toolkit Params

| Param                         | Type        | Default | Description                                                                        |
| ----------------------------- | ----------- | ------- | ---------------------------------------------------------------------------------- |
| `get_video_captions`          | `bool`      | `True`  | Enables the functionality to retrieve video captions.                              |
| `get_video_data`              | `bool`      | `True`  | Enables the functionality to retrieve video metadata and other related data.       |
| `languages`                   | `List[str]` | -       | Specifies the list of languages for which data should be retrieved, if applicable. |
| `enable_get_video_captions`   | `bool`      | `True`  | Enable the get\_video\_captions functionality.                                     |
| `enable_get_video_data`       | `bool`      | `True`  | Enable the get\_video\_data functionality.                                         |
| `enable_get_video_timestamps` | `bool`      | `True`  | Enable the get\_video\_timestamps functionality.                                   |
| `all`                         | `bool`      | `False` | Enable all functionality.                                                          |

## Toolkit Functions

| Function                       | Description                                                |
| ------------------------------ | ---------------------------------------------------------- |
| `get_youtube_video_captions`   | This function retrieves the captions of a YouTube video.   |
| `get_youtube_video_data`       | This function retrieves the metadata of a YouTube video.   |
| `get_youtube_video_timestamps` | This function retrieves the timestamps of a YouTube video. |

## Developer Resources

* View [Tools](https://github.com/agno-agi/agno/blob/main/libs/agno/agno/tools/youtube.py)
