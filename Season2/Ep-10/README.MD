## **\*\*\*\***\***\*\*\*\***Advance authentication technique**\*\*\*\***\*\*\***\*\*\*\***

- whenever we make a login http request the server validate email and password after that the server create a Jwt token and this token is passed into the cookie and send back to the client.
- what is cokkie?
- what is jwt?=>header,payload,signature varification(optional)
- how do you sign and verify these jwt tokens?
  =>creating a token
  =>validating a token
  =>decoding the message from it
  =>returning the data from it.

- basically when we logged in, then server responds a cookie with token in it,most probably we keep the user_id in it and whenever we make another api call like get profile then this is sent along with the api request and at the server this token is verified by the jwt.verify function and it will give us decoded message where (\_id) is present and from this (\_id) ,server can get the user data from the database and can send it back to the client.

- learn about schema methods=>on the instance of the model(on a single user document) and schema static=>static methods(on the whole model).
