# Trello API

**Description:** I created boards, lists and cards on Trello using APIs and Postman. 
<br>

<a href="https://developer.atlassian.com/cloud/trello/rest/api-group-actions/" target="_blank">API Documentation</a> 
<br><br>

**CREATE NEW COLLECTION**
<p>
I created new collection in Postman app. <br>
Collection's name: Trello. <br>
  
**Variables:** <br>
{{baseurl}} = https://api.trello.com <br><br>
  
**CREATE A NEW BOARD**
`POST` 
/1/boards/
<br>

**Query params:**
  - name: API Board
  - key
  - token

Status: 200 OK <br>
Result: The "API Board" was created.
<br><br>
  
**GET BOARDS THAT MEMBER BELONGS TO**
`GET`
/1/members/me/boards
<br>

**Query params:**
  - key
  - token

Status: 200 OK <br>
Result: I got the list of all my boards. "API Board" ID is 63e66c84d9e22ffc54d7c267.
<br><br>
  
**CREATE A LIST ON A BOARD**
`POST` 
/1/boards/{id}/lists
  
**Query params:**
- board ID: 63e66c84d9e22ffc54d7c267
- list name: In progress
- key
- token

Status: 200 OK <br>
Result: _A "In Progress" list was created with ID 63e6b255a9038a48f879f22c._ <br><br>
  
**GET LISTS ON A BOARD**
`GET` 
/1/boards/{id}/lists
<br>

**Query params:**
- ID of the board: 63e66c84d9e22ffc54d7c267
- key
- token

Status: 200 OK <br>
Result: I got the lists on the API Board - "To Do", "In Progress", "Doing" and "Done"
  
**CREATE A NEW CARD**
`POST` 
/1/cards?idList={id}
<br>

**Query params:**
- ID of the list: 63e6b255a9038a48f879f22c
- name: There's a card name
- desc: You can write a description here
- key
- token

Status: 200 OK <br>
Result: _A new card was created with ID 63e75259e839c8cee7a01029. <br><br>

**GET CARDS ON A BOARD**
`GET`
/1/boards/{id}/cards
<br>

**Query params:**
- ID of the board: 63e66c84d9e22ffc54d7c267
- key
- token
  
Status: 200 OK <br>
Result: I got a list of cards on the API Board. <br><br>
  
**UPDATE A CARD**
`PUT` 
/1/cards/{id}
<br>
  
**Query params:**
- ID of the board: 63e66c84d9e22ffc54d7c267
- name: Update name
- desc: Update description
- key
- token

Status: 200 OK <br>
Result: The name and description of the card were changed. <br><br>
