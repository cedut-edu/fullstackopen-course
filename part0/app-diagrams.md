# 0.4: New note diagram

```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server

    Note right of browser: The text typed in the form is sent in the body of the request

    Note left of server: The server saves the data in a database and responds with a redirect

    server-->>browser: Redirect to notes. Status code: 302 Found
    deactivate server

    Note left of server: Response header: Location: /exampleapp/notes

    Note right of browser: The browser receives the response and redirects the user to the address in the Location header

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{"content":"HTML is easy","date":"2019-05-23T17:30:31.098Z"}, ... ]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes
```

# 0.5: Single page app diagram

```mermaid
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser executes the callback function that renders the notes
```

# 0.6: New note in Single page app diagram

```mermaid
sequenceDiagram
    participant browser
    participant server

    Note right of browser: The form's submit handler calls preventDefault(), so the page does not reload

    Note right of browser: The JavaScript creates the note object (content and date), adds it to the local list, clears the input field and redraws the list on screen

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
    activate server

    Note right of browser: Request header: Content-Type: application/json. Body: {"content": "note text", "date": "2023-1-1"}

    server-->>browser: Status code: 201 Created, {"message":"note created"}
    deactivate server

    Note right of browser: The browser does not reload the page or make new GET requests. The answer is only shown on the screen
```