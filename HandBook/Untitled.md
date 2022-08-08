# Room Database

It is an abstract of mysql database. It makes things simple from mySql database.

It contains 3 components:

1. Database (abstract class extending **RoomDatabase**)
2. Entity (Represents table in Database)
3. DAO (Every Entity needs a DAO (Data Access Object) Interface, It contains functions to access or manupolate our database)