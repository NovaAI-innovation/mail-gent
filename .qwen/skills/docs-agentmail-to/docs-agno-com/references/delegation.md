# Delegation

**Source:** https://docs.agno.com/teams/delegation.md
**Section:** Docs

**Description:** Control how the team leader delegates tasks to members.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Delegation

> Control how the team leader delegates tasks to members.

When you call `run()` on a team, the leader decides how to handle the request: respond directly, use tools, or delegate to members.

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-light.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=2ee1ac8bf7774125e30b2f8a8ba5e0e5" alt="Team delegation flow" data-og-width="4353" width="4353" data-og-height="1233" height="1233" data-path="images/teams/team-delegate-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-light.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=c916681a232cce0726b37ff11231199c 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-light.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=b969c1ebdafcf0a396919831b66e5705 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-light.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=71f8372710764574ec6c1a90077e2b32 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-light.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=74343688fc677499b5cbf5c4561aec65 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-light.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=8d9a72eaad258842d959f0a29124dba0 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-light.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=cc4d6396915b59c137aadd29eab708c3 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-dark.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=75634aa1f580bf358dafee8c7e114d85" alt="Team delegation flow" data-og-width="4353" width="4353" data-og-height="1233" height="1233" data-path="images/teams/team-delegate-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-dark.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=7c700427d1047a065738303c582321da 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-dark.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=e1df59a26d24fc7b73b489264700bed1 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-dark.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=9fc3130ac1b144e34ef120ca627b6a9d 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-dark.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=e4670efd70404a5dc612e89a81e01850 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-dark.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=550dac3bfceea50fa94481a8562b5851 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-dark.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=4d0a1bbeba92f6b5a4d5f02d2d57084f 2500w" />

The default flow:

1. Team receives user input
2. Leader analyzes the input and decides which members to delegate to
3. Leader formulates a task for each selected member
4. Members execute and return results (concurrently in async mode)
5. Leader synthesizes results into a final response

You can customize this flow with three patterns:

| Pattern                  | Configuration                                                 | Behavior                                                      |
| ------------------------ | ------------------------------------------------------------- | ------------------------------------------------------------- |
| **Supervisor** (default) | Default settings                                              | Leader selects members, formulates tasks, synthesizes results |
| **Router**               | `respond_directly=True` + `determine_input_for_members=False` | Leader routes to member, returns member response directly     |
| **Broadcast**            | `delegate_to_all_members=True`                                | Leader delegates to all members simultaneously                |

## Supervisor Pattern (Default)

The leader controls everything: which members to use, what task to give them, and how to combine their outputs.

```python  theme={null}
from agno.team import Team
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.hackernews import HackerNewsTools
from agno.tools.yfinance import YFinanceTools

team = Team(
    name="Research Team",
    model=OpenAIResponses(id="gpt-4o"),
    members=[
        Agent(name="News Agent", role="Get tech news", tools=[HackerNewsTools()]),
        Agent(name="Finance Agent", role="Get stock data", tools=[YFinanceTools()])
    ],
    instructions="Research the topic thoroughly, then synthesize findings into a clear report."
)

team.print_response("What's happening with AI companies and their stock prices?")
```

Use this when:

* Tasks need decomposition into subtasks
* You want quality control over the final output
* The leader should add context or reasoning to member outputs

## Router Pattern

The leader selects which member handles the request, then passes the request through unchanged and returns the member's response directly.

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-light.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=badf1c510d5f4ba340d79a775e83bd40" alt="Router pattern flow" data-og-width="3609" width="3609" data-og-height="906" height="906" data-path="images/teams/team-passthrough-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-light.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=2bd0c59b87682466cd66309cd92ebd03 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-light.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=20d283af99676207613721b65a1544da 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-light.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=739d74525339750620fa0367d25b659d 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-light.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=f6e388ccdcabf2efbd24e818c8836760 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-light.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=c0580f40db044da51acf1c8076da06dc 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-light.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=805e9091813e45cba058ecb5d9421b31 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-dark.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=a6a7cb2997cea9eae541f879d2cce9be" alt="Router pattern flow" data-og-width="3609" width="3609" data-og-height="906" height="906" data-path="images/teams/team-passthrough-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-dark.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=bcef71b578dd4919ea49363e02e6733c 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-dark.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=0200cac28e7a126209261fcd12f07b9a 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-dark.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=a7deb75d871986bba5cfba09e5a67a82 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-dark.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=c34e7dda68f025a197beafce99eb2c4f 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-dark.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=b2f1f4ace92edee11d28ef4c1332dc56 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-passthrough-dark.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=f9c97b3a73e143f20db785edfa1009df 2500w" />

```python  theme={null}
from agno.team import Team
from agno.agent import Agent
from agno.models.openai import OpenAIResponses

team = Team(
    name="Language Router",
    model=OpenAIResponses(id="gpt-4o"),
    members=[
        Agent(name="English Agent", role="Answer questions in English"),
        Agent(name="Japanese Agent", role="Answer questions in Japanese"),
    ],
    respond_directly=True,            # Return member response without synthesis
    determine_input_for_members=False # Pass user input unchanged to member
)

team.print_response("How are you?")        # Routes to English Agent
team.print_response("お元気ですか?")        # Routes to Japanese Agent
```

Use this when:

* You have specialized agents and want automatic routing
* The leader shouldn't modify the request or response
* You want lower latency (no synthesis step)

### Configuration Options

**`respond_directly=True`**: Return member responses without leader synthesis.

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-light.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=a855fa91b944dceb3789755b812fe5c2" alt="Direct response flow" data-og-width="3741" width="3741" data-og-height="906" height="906" data-path="images/teams/team-direct-response-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-light.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=27e35955cb85dca4bc71dc1d1dfbbf29 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-light.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=387ba410b479f59b05223337345e5718 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-light.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=dce5fcec7a3430097af30350ac8b5553 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-light.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=3d998291345023788b76061af03957d9 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-light.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=af7a76b687b05506b17216021005ba6b 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-light.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=915198cecad6c4257b3d4e83fc07cf91 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-dark.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=d9e2544a995856e07934634987e04b19" alt="Direct response flow" data-og-width="3741" width="3741" data-og-height="906" height="906" data-path="images/teams/team-direct-response-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-dark.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=173929609381c8ea1e48f47a139f9b67 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-dark.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=8824c3afb76ad9cdabb91aee3e90349d 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-dark.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=c8e7b3a1a78a34a3433bd5a8cffabb1c 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-dark.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=76bee7fe4ec738d466d3c4eeac29aff5 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-dark.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=61b1e5c2dd13a193a9c06eb2635f3bf5 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-direct-response-dark.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=f97f8c756fbdfab1a16a00f3c79f6c81 2500w" />

**`determine_input_for_members=False`**: Send user input directly to members instead of having the leader formulate a task.

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-light.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=50e30700e0ab7e2dee727e085960825a" alt="Raw input flow" data-og-width="4896" width="4896" data-og-height="906" height="906" data-path="images/teams/team-raw-input-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-light.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=0915e2f2d4c1b30d9b7617f2225dd597 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-light.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=c6f8a0bb2ea0872d494c591cd797c20f 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-light.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=ba0fb4acdd28b52c72b5e990e9290252 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-light.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=fbc8d51f02a5f844ddca981e45b37f8d 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-light.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=7b3f4e882827ed6dcf70345bc629d15e 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-light.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=93a164ca96e5c33a1c7b7d46961c69c5 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-dark.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=e3d140d90d77da02c526c606c9446a52" alt="Raw input flow" data-og-width="4896" width="4896" data-og-height="906" height="906" data-path="images/teams/team-raw-input-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-dark.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=88866626fd38333a840b7737a79b31d9 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-dark.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=090e93bb46d57b37465123d3e97242ff 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-dark.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=dc7f8458ae6685266454c72485ccedf7 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-dark.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=941c0045feaec734857677b822a17e2a 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-dark.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=04eba2381d53da383c59061d6eaf67db 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-raw-input-dark.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=afe6376289414c8e72dedf7f17c19483 2500w" />

Combine both for a full passthrough:

```python  theme={null}
team = Team(
    respond_directly=True,
    determine_input_for_members=False,
    ...
)
```

## Broadcast Pattern

The leader delegates to all members at once. Useful for gathering multiple perspectives or parallel research.

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-light.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=9db7cc875ebf53fc88ce5ef5ad900eb1" alt="Broadcast pattern flow" data-og-width="3699" width="3699" data-og-height="906" height="906" data-path="images/teams/team-delegate-to-all-members-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-light.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=aa883551877111ae04389715768858e1 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-light.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=17e3d965ad7e1699081fdec8df976b4d 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-light.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=9609c9fa6cd91de68eabd6d0ba752e50 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-light.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=9365f145a3b2c095dfce87e6fb66a2c1 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-light.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=44d0fa282146382ac1b63a8036b3739e 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-light.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=cda8e9cdf36e8a3bdef2fe40e9351e38 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-dark.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=58079bd5c2876131bdc5c06da5dd2b8f" alt="Broadcast pattern flow" data-og-width="3699" width="3699" data-og-height="906" height="906" data-path="images/teams/team-delegate-to-all-members-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-dark.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=5ef4938505de546fca41134253e9d636 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-dark.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=16ff138ca601bc09bcf371264c750cc0 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-dark.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=265b89ce2ed4d56fdfbe4fff603a8533 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-dark.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=fef810682777a8081b4496796eadbdb7 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-dark.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=46cba6e4f62cc93ab4d13668bd9e4186 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-delegate-to-all-members-dark.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=da02200336382ce04305b7986dba78fe 2500w" />

```python  theme={null}
import asyncio
from agno.team import Team
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.hackernews import HackerNewsTools
from agno.tools.arxiv import ArxivTools
from agno.tools.duckduckgo import DuckDuckGoTools

team = Team(
    name="Research Team",
    model=OpenAIResponses(id="gpt-4o"),
    members=[
        Agent(name="HackerNews Researcher", role="Find discussions on HackerNews", tools=[HackerNewsTools()]),
        Agent(name="Academic Researcher", role="Find academic papers", tools=[ArxivTools()]),
        Agent(name="Web Researcher", role="Search the web", tools=[DuckDuckGoTools()]),
    ],
    delegate_to_all_members=True,
    instructions="Synthesize findings from all researchers into a comprehensive report."
)

# Use async for concurrent execution
asyncio.run(team.aprint_response("Research the current state of AI agents"))
```

Use this when:

* You want multiple perspectives on the same topic
* Members can work independently
* Parallel execution improves latency

<Note>
  `delegate_to_all_members=True` is not compatible with `respond_directly=True`.
</Note>

## Structured Input

When using `determine_input_for_members=False`, you can pass structured Pydantic models directly to members:

```python  theme={null}
from pydantic import BaseModel, Field
from agno.team import Team
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.hackernews import HackerNewsTools

class ResearchRequest(BaseModel):
    topic: str
    num_sources: int = Field(default=5)

research_agent = Agent(
    name="Research Agent",
    role="Research topics on HackerNews",
    tools=[HackerNewsTools()]
)

team = Team(
    name="Research Team",
    model=OpenAIResponses(id="gpt-4o"),
    members=[research_agent],
    determine_input_for_members=False  # Pass input directly to member
)

request = ResearchRequest(topic="AI Agents", num_sources=10)
team.print_response(input=request)
```

## Production Considerations

### Token Costs

Each pattern has different token overhead:

| Pattern    | Coordination Cost                | When to Use                              |
| ---------- | -------------------------------- | ---------------------------------------- |
| Supervisor | High (decomposition + synthesis) | Quality matters more than cost           |
| Router     | Low (selection only)             | Simple routing, cost-sensitive           |
| Broadcast  | Medium (synthesis only)          | Parallel research, multiple perspectives |

### Latency

* **Supervisor**: Sequential (leader thinks → members execute → leader synthesizes)
* **Router**: Fast (leader selects → member executes)
* **Broadcast with async**: Parallel member execution, but synthesis adds latency

### Error Handling

What happens when a member fails?

* **Supervisor**: Leader can work with partial results from other members
* **Router**: Failure is returned directly to caller
* **Broadcast**: Leader synthesizes available results, may note missing data

## Developer Resources

* [Team reference](/reference/teams/team)
* [Team examples](/cookbook/teams/overview)
