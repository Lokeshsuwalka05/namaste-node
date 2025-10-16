- Schema pre before saving a document in the database.
- using indexes in database to query fast to retrieve a document from the database.if your database becomes huge after that for a single document retrieval from the database it takes so much time to find it.
- so for this purpose use indexes in your database.
- always put index on that field which is very important.let's take an example 
  =>in login api we are finding the user by email id.if you are not keeping index for emailId then it will take time to retrieve it from the database but after using indexes it becomes very fast;
- when you do (unique:true) for a field then it will automatically take index for that field.so i don't worry about efficiency to retrieve it from database.
- 
An enum (enumeration) is a special data type that allows a variable to take one of a predefined set of named values, improving code readability, maintainability, and type safety.

In TypeScript / Java / C++ → Enum is a proper data type with fixed named constants.

In JavaScript → Enum is simulated using objects or frozen objects to represent fixed values.

In MongoDB (Mongoose schema) → Enum is defined as an array of allowed values to validate field input.
