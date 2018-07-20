# Qualaroo over iFrame

## Making API Calls

All Qualaroo Javascript API methods are available via sending a messsage to the frame.

When loading the iframe a unique ID should be provided via the `cid` URL param. This ID will be included in all message payloads back to the parent page (see "Events" below).

Message format:

````
["roo:[METHOD NAME]", args ...]
````

For example, instead of calling:

````
window._kiq.push(['showSurvey', '1234', true]);
````

You call:

````
frame.postMessage(['roo:showSurvey', '1234', true], '*');
````

## Events

The Qualaroo frame will return the following events via message to the parent page.

| Event                    | Description                                                                                                |
| ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| `roo:event:ready`        | The Qualaroo client has loaded in the frame and is ready to receive messages.                              |
| `roo:event:show`         | A survey is displayed to the user. Returned arguments: `survey_id`                                         |
| `roo:event:submit`       | A user has submitted an answer to a question. Returned arguments: `answers, survey_id, question_id`        |
| `roo:event:nodeRendered` | Qualaroo rendered a screen (question, message). Returned arguments: `survey_id, screen_id, width, height`  |

Message format:

````
["[CHANNEL ID]", "roo:event:[EVENT NAME]", args ...]
````
