JSON-Server provides a mock of a REST API mocking based on plain JSON. The data on json are easy to edit to reflect the data we want to render on front-end.

To run the mock api just run this command on the terminal:

```docker run -p 5000:80 -v $(pwd)/backend/db.json:/data/db.json --name json-server clue/json-server```

Then to access the api from the browser: `http://localhost:5000/tasks`