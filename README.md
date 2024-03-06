# Smart Notes API QuickStart

The aim of this document is to provide developers with all the pieces of information they need to integrate Smart Notes to their platform.

## Table of Contents

- [Overview](#overview)
- [Authentication](#authentication)
- [Read contents](#read-contents)

## Overview

Smart Notes APIs provide partners with the ability to integrate the data processed by Smart Notes in their own application.

To get access to the API you must first purchase a Smart Notes license.

Smart Notes APIs are based on the [GraphQL Protocol](https://graphql.org).

The API endpoint is `https://api.smart-notes.extrai.app/v1/graphql`

The list of the available APIs and the exchanged models, can be accessed via GraphQL playground:

`https://api.smart-notes.extrai.app/v1/graphql/playground`

## Authentication

All requests to Smart Notes APIs must be authenticated.

The APIs are exclusively meant to be used in a _server to server_ environment, as they are authenticated via API Key.

### Generate API Key

Login into [Smart Notes Manager](https://manager.smart-notes.extrai.app) app, open the side menu and click on `API`, then follow the instructions to generate a new API key.

## Read contents

### Run queries via GraphQL Playground

1. Open the GraphQL Playground `https://api.smart-notes.extrai.app/v1/graphql/playground`
2. Add the API Key header in the bottom `Headers` input
    ```json
    {
        "X-API-Key": "insertYourAPIKeyHere"
    }
    ```
3. Use the following queries to get the list of available contents or a single content

#### Get the list of contents

```graphql
query getContents{
  getContents(pagination: {
    offset: 0
    first: 10
  }){
    totalCount
    edges{
      node{
        id
        name
        keyPointsGenerationProcessStatus
        keyPointsTranslationProcessStatus
        keyPointsLocale
        keyPoints{
          title
          text
          localizedData{
            locale
            title
            text
          }
        }
        data{
          ... on Lesson{
            speakers{
              name
              bio
            }
          }
          ... on Talk{
            startAt
            speakers{
              name
              bio
            }
          }
        }
        references{
          id
          url
          localizedDisplayText{
            locale
            displayText
          }
        }
      }
    }
    pageInfo{
      offset
      first
      scrollID
    }
  }
}
```

#### Get a single content

```graphql
query getContent{
  getContent(contentID: "insertYourContentIDHere") {
    id
    name
    keyPointsGenerationProcessStatus
    keyPointsTranslationProcessStatus
    keyPointsLocale
    keyPoints{
      title
      text
      localizedData{
        locale
        title
        text
      }
    }
    data{
      ... on Lesson{
        speakers{
          name
          bio
        }
      }
      ... on Talk{
        startAt
        speakers{
          name
          bio
        }
      }
    }
    references{
      id
      url
      localizedDisplayText{
        locale
        displayText
      }
    }
  }
}
```

### Run queries via Python

#### Get the list of contents

```python
import requests

url = 'https://api.smart-notes.extrai.app/v1/graphql'
api_key = 'insertYourAPIKeyHere'

query = """
query getContents{
  getContents(pagination: {
    offset: 0
    first: 10
  }){
    totalCount
    edges{
      node{
        id
        name
        keyPointsGenerationProcessStatus
        keyPointsTranslationProcessStatus
        keyPointsLocale
        keyPoints{
          title
          text
          localizedData{
            locale
            title
            text
          }
        }
        data{
          ... on Lesson{
            speakers{
              name
              bio
            }
          }
          ... on Talk{
            startAt
            speakers{
              name
              bio
            }
          }
        }
        references{
          id
          url
          localizedDisplayText{
            locale
            displayText
          }
        }
      }
    }
    pageInfo{
      offset
      first
      scrollID
    }
  }
}
"""

headers = {
    'X-API-Key': api_key
}

response = requests.post(url, json={'query': query}, headers=headers)

if response.status_code == 200:
    print(response.text)
else:
    print("HTTP response status code:", response.status_code)
    print(response.text)
```

#### Get a single content

```python
import requests

url = 'https://api.smart-notes.extrai.app/v1/graphql'
api_key = 'insertYourAPIKeyHere'
content_id = 'insertYourContentIDHere'

query = """
query getContent{
  getContent(contentID: "%s") {
    id
    name
    keyPointsGenerationProcessStatus
    keyPointsTranslationProcessStatus
    keyPointsLocale
    keyPoints{
      title
      text
      localizedData{
        locale
        title
        text
      }
    }
    data{
      ... on Lesson{
        speakers{
          name
          bio
        }
      }
      ... on Talk{
        startAt
        speakers{
          name
          bio
        }
      }
    }
    references{
      id
      url
      localizedDisplayText{
        locale
        displayText
      }
    }
  }
}
""" % (content_id)

headers = {
    'X-API-Key': api_key
}

response = requests.post(url, json={'query': query}, headers=headers)

if response.status_code == 200:
    print(response.text)
else:
    print("HTTP response status code:", response.status_code)
    print(response.text)
```
