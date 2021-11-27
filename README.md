# Vue task manager

This is a crash [course](https://www.youtube.com/watch?v=qZXt1Aom3Cs) on Vue.js from Traversy Media, creating a task manager app. The app has some basic crud functionality such as creating a new task, showing all tasks, deleting a task and adding or removing a reminder.

### Useful commands
1. To create a new vue app: <br>
   1.1 Build the image: `docker build . -t vue-cli -f Dockerfile.create`<br>
   1.2 Create a new app with cli `docker run -itd -v ${PWD}:/app --name create_vue vue-cli` and then
   `docker exec -it create_vue vue create .`<br>
   1.3 Stop the running container `docker stop create_vue`
2. To launch the app using Docker: `docker-compose up`
3. To launch json-server using docker: `docker run -p 5000:80 -v $(pwd)/backend/db.json:/data/db.json --name json-server clue/json-server`
4. To stop json-server: `docker stop json-server` and then `docker rm json-server`
5. To run npm commands within the app container: `docker exec -it vue_crash sh`