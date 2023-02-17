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

Status: 200 OK
<br><br>
  
**GET BOARDS THAT MEMBER (ME) BELONGS TO**
`GET`
/1/members/me/boards
<br>

**Query params:**
  - key
  - token

Status: 200 OK
<br><br>
  
**CREATE A LIST ON A BOARD**
`POST` 
/1/boards/{id}/lists
_ID board get from the GET Boards request: 63e66c84d9e22ffc54d7c267_
  
**Query params:**
- list name: In progress
- key
- token

_It was created the "In Progress" list that ID is 63e6b255a9038a48f879f22c._

Status: 200 OK <br><br>
