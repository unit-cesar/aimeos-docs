This article contains all actions for retrieving and managing rules.

# Get rule by ID

=== "Query"
    ```graphql
    query {
      getRule(id: "1") {
        id
        siteid
        type
        label
        provider
        datestart
        dateend
        config
        position
        status
        mtime
        ctime
        editor
      }
    }
    ```
=== "Javascript"
    ```javascript
    const body = JSON.stringify({'query':
    `query {
      getRule(id: "1") {
        id
        siteid
        type
        label
        provider
        datestart
        dateend
        config
        position
        status
        mtime
        ctime
        editor
      }
    }`});

    fetch($('.aimeos').data('graphql'), {
        method: 'POST',
        credentials: 'same-origin',
        headers: { // Laravel only
            'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
        },
        body: body
    }).then(response => {
        return response.json();
    }).then(data => {
        console.log(data);
    });
    ```

Response:

```json
{
  "data": {
    "getRule": {
      "id": "1",
      "siteid": "1.",
      "type": "catalog",
      "label": "+10% Test",
      "provider": "Percent",
      "datestart": null,
      "dateend": null,
      "config": "{\"last-rule\":0,\"percent\":10}",
      "position": 0,
      "status": 1,
      "mtime": "2022-12-22 09:51:38",
      "ctime": "2022-06-21 13:36:28",
      "editor": "aimeos@aimeos.org"
    }
  }
}
```

# Search rules

The filter parameter is explained in the [filter section](basics.md#filtering-the-result) of the [GraphQL basics](basics.md) article.

=== "Query"
    ```graphql
    query {
      searchRules(filter: "{\"~=\": {\"rule.label\":\"Test\"}}") {
        id
        siteid
        type
        label
        provider
        datestart
        dateend
        config
        position
        status
        mtime
        ctime
        editor
      }
    }
    ```
=== "Javascript"
    ```javascript
    let filter = {
        "~=": {"rule.label":"Test"}
    };
    const fstr = JSON.stringify(filter).replace(/"/g, '\\"');
    const body = JSON.stringify({'query':
    `query {
      searchRules(filter: "` + fstr + `") {
        id
        siteid
        type
        label
        provider
        datestart
        dateend
        config
        position
        status
        mtime
        ctime
        editor
      }
    }`});

    fetch($('.aimeos').data('graphql'), {
        method: 'POST',
        credentials: 'same-origin',
        headers: { // Laravel only
            'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
        },
        body: body
    }).then(response => {
        return response.json();
    }).then(data => {
        console.log(data);
    });
    ```

Response:

```json
{
  "data": {
    "searchRules": [
      {
        "id": "1",
        "siteid": "1.",
        "type": "catalog",
        "label": "+10% Test",
        "provider": "Percent",
        "datestart": null,
        "dateend": null,
        "config": "{\"last-rule\":0,\"percent\":10}",
        "position": 0,
        "status": 1,
        "mtime": "2022-12-22 09:51:38",
        "ctime": "2022-06-21 13:36:28",
        "editor": "aimeos@aimeos.org"
      }
    ]
  }
}
```

# Save single rule

=== "Mutation"
    ```graphql
    mutation {
      saveRule(input: {
        type: "catalog"
        label: "Test rule"
        provider: "Percent"
        config: "{\"percent\": 10}"
      }) {
        id
      }
    }
    ```
=== "Javascript"
    ```javascript
    const body = JSON.stringify({'query':
    `mutation {
      saveRule(input: {
        type: "catalog"
        label: "Test rule"
        provider: "Percent"
        config: "{\"percent\": 10}"
      }) {
        id
      }
    }`});

    fetch($('.aimeos').data('graphql'), {
        method: 'POST',
        credentials: 'same-origin',
        headers: { // Laravel only
            'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
        },
        body: body
    }).then(response => {
        return response.json();
    }).then(data => {
        console.log(data);
    });
    ```

Response:

```json
{
  "data": {
    "saveRule": {
      "id": "2"
    }
  }
}
```

# Save multiple rules

=== "Mutation"
    ```graphql
    mutation {
      saveRules(input: [{
        type: "catalog"
        label: "Test rule 2"
        provider: "Percent"
        config: "{\"percent\": 10}"
      },{
        type: "catalog"
        label: "Test rule 3"
        provider: "Percent,Category"
        config: "{\"percent\":20,\"category.code\":\"demo-best\"}"
      }]) {
        id
      }
    }
    ```
=== "Javascript"
    ```javascript
    const body = JSON.stringify({'query':
    `mutation {
      saveRules(input: [{
        type: "catalog"
        label: "Test rule 2"
        provider: "Percent"
        config: "{\"percent\": 10}"
      },{
        type: "catalog"
        label: "Test rule 3"
        provider: "Percent,Category"
        config: "{\"percent\":20,\"category.code\":\"demo-best\"}"
      }]) {
        id
      }
    }`});

    fetch($('.aimeos').data('graphql'), {
        method: 'POST',
        credentials: 'same-origin',
        headers: { // Laravel only
            'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
        },
        body: body
    }).then(response => {
        return response.json();
    }).then(data => {
        console.log(data);
    });
    ```

Response:

```json
{
  "data": {
    "saveRules": [
      {
        "id": "3"
      },
      {
        "id": "4"
      }
    ]
  }
}
```

# Delete single rule

=== "Mutation"
    ```graphql
    mutation {
      deleteRule(id: "2")
    }
    ```
=== "Javascript"
    ```javascript
    const body = JSON.stringify({'query':
    `mutation {
      deleteRule(id: "2")
    }`});

    fetch($('.aimeos').data('graphql'), {
        method: 'POST',
        credentials: 'same-origin',
        headers: { // Laravel only
            'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
        },
        body: body
    }).then(response => {
        return response.json();
    }).then(data => {
        console.log(data);
    });
    ```

Response:

```json
{
  "data": {
    "deleteRule": "2"
  }
}
```

# Delete multiple rules

=== "Mutation"
    ```graphql
    mutation {
      deleteRules(id: ["3", "4"])
    }
    ```
=== "Javascript"
    ```javascript
    const body = JSON.stringify({'query':
    `mutation {
      deleteRules(id: ["3", "4"])
    }`});

    fetch($('.aimeos').data('graphql'), {
        method: 'POST',
        credentials: 'same-origin',
        headers: { // Laravel only
            'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
        },
        body: body
    }).then(response => {
        return response.json();
    }).then(data => {
        console.log(data);
    });
    ```

Response:

```json
{
  "data": {
    "deleteRules": [
      "3",
      "4"
    ]
  }
}
```
